- [Tạo LangGraph dùng Mistral local](#tạo-langgraph-dùng-mistral-local)
- [Multiple Nodes \& Flow thật sự của LangGraph](#multiple-nodes--flow-thật-sự-của-langgraph)
- [Build Agent Loop](#build-agent-loop)
- [Mini Agent tiếng việt có tool + loop](#mini-agent-tiếng-việt-có-tool--loop)
- [Thiết kế kiến trúc cho Website AI Agent](#thiết-kế-kiến-trúc-cho-website-ai-agent)
---
# Tạo LangGraph dùng Mistral local
```bash
from typing import TypedDict
from langgraph.graph import StateGraph, END
from langchain_community.chat_models import ChatOllama

# 1️⃣ Kết nối Mistral local
llm = ChatOllama(model="mistral")

# 2️⃣ State
class MyState(TypedDict):
    question: str
    answer: str

# 3️⃣ Node dùng LLM
def llm_node(state: MyState):
    response = llm.invoke(state["question"])
    return {"answer": response.content}

# 4️⃣ Build graph
graph = StateGraph(MyState)

graph.add_node("llm", llm_node)
graph.set_entry_point("llm")
graph.add_edge("llm", END)

app = graph.compile()

# 5️⃣ Test
result = app.invoke({"question": "Explain AI simply"})
print(result["answer"])
```
# Multiple Nodes & Flow thật sự của LangGraph
```python
from typing import TypedDict
from langgraph.graph import StateGraph, END
from langchain_community.chat_models import ChatOllama

llm = ChatOllama(model="mistral")

class MyState(TypedDict):
    question: str
    answer: str

# Node 1: decide
def decide_node(state: MyState):
    if len(state["question"]) < 20:
        return "simple"
    else:
        return "detailed"

# Node 2: simple answer
def simple_node(state: MyState):
    response = llm.invoke("Answer briefly: " + state["question"])
    return {"answer": response.content}

# Node 3: detailed answer
def detailed_node(state: MyState):
    response = llm.invoke("Answer in detail: " + state["question"])
    return {"answer": response.content}

# Build graph
graph = StateGraph(MyState)

graph.add_node("simple", simple_node)
graph.add_node("detailed", detailed_node)

graph.set_conditional_entry_point(decide_node)

graph.add_edge("simple", END)
graph.add_edge("detailed", END)

app = graph.compile()

# Test
result = app.invoke({"question": "What is AI?"})
print(result["answer"])
```
# Build Agent Loop
```bash
START
  ↓
reason
  ↓
(decide done?)
   ↙        ↘
  NO        YES
   ↓         ↓
  tool      END
   ↓
 reason (lặp lại)
```
```python
from typing import TypedDict
from langgraph.graph import StateGraph, END

class MyState(TypedDict):
    count: int

def loop_node(state: MyState):
    print("Current:", state["count"])
    return {"count": state["count"] + 1}

def should_continue(state: MyState):
    if state["count"] >= 2:
        return END
    return "loop"

graph = StateGraph(MyState)

graph.add_node("loop", loop_node)

graph.set_entry_point("loop")
graph.add_conditional_edges("loop", should_continue)

app = graph.compile()

app.invoke({"count": 0})
```
# Mini Agent tiếng việt có tool + loop
```bash
Agent sẽ:
    1. Nhận câu hỏi
    2. Suy nghĩ
    3. Nếu cần tính toán → dùng tool tính toán
    4. Nếu đủ thông tin → trả lời
    5. Nếu chưa → tiếp tục suy nghĩ
```
**Flow**
```bash
START
  ↓
suy_nghi
  ↓
(quyết định)
  ↙          ↘
dùng_tool     kết_thúc
  ↓
suy_nghi (lặp)
```
```python
from typing import TypedDict
from langgraph.graph import StateGraph, END
from langchain_community.chat_models import ChatOllama

llm = ChatOllama(model="mistral")

# 1️⃣ State
class AgentState(TypedDict):
    cau_hoi: str
    suy_nghi: str
    ket_qua_tool: str
    tra_loi: str

# 2️⃣ Tool đơn giản: máy tính
def may_tinh(phep_tinh: str):
    try:
        return str(eval(phep_tinh))
    except:
        return "Không tính được"

# 3️⃣ Node suy nghĩ
def node_suy_nghi(state: AgentState):
    prompt = f"""
    Bạn là AI. 
    Câu hỏi: {state['cau_hoi']}
    
    Nếu cần tính toán, hãy trả về:
    TOOL: phép_tính
    
    Nếu đã đủ thông tin, hãy trả về:
    FINAL: câu_trả_lời
    """

    response = llm.invoke(prompt)
    output = response.content

    if "TOOL:" in output:
        phep_tinh = output.split("TOOL:")[1].strip()
        return {"suy_nghi": phep_tinh}
    else:
        final_answer = output.split("FINAL:")[-1].strip()
        return {"tra_loi": final_answer}

# 4️⃣ Node dùng tool
def node_tool(state: AgentState):
    ket_qua = may_tinh(state["suy_nghi"])
    return {"ket_qua_tool": ket_qua}

# 5️⃣ Quyết định rẽ nhánh
def dieu_huong(state: AgentState):
    if state.get("tra_loi"):
        return END
    return "tool"

# 6️⃣ Build graph
graph = StateGraph(AgentState)

graph.add_node("suy_nghi", node_suy_nghi)
graph.add_node("tool", node_tool)

graph.set_entry_point("suy_nghi")

graph.add_conditional_edges("suy_nghi", dieu_huong)
graph.add_edge("tool", "suy_nghi")

app = graph.compile()

# 7️⃣ Test
result = app.invoke({
    "cau_hoi": "15 nhân 3 bằng bao nhiêu?"
})

print("Trả lời:", result["tra_loi"])
```
# Thiết kế kiến trúc cho Website AI Agent
```bash
User
  ↓
Memory
  ↓
Intent Planner (LLM quyết định hành động)
  ↓
( Tool Router )
  ↓
Tool thực thi (DB / API / Logic)
  ↓
Response Generator
  ↓
Save Memory
```
**Step 1: Phân loại tool**
```bash
Website thường có 3 nhóm tool:
    1. User Tools (cần user_id)
        - get_user_profile
        - get_user_orders
        - update_user_info
    2. Business Logic Tools
        - recommend_food
        - calculate_price
        - check_inventory
    3. Pure LLM Response
        - Giải thích
        - Tư vấn
        - Trò chuyện
```