- [graph](#graph)
  - [StateGraph (Tạo graph với state kiểu TypeDict)](#stategraph-tạo-graph-với-state-kiểu-typedict)
    - [Create \& Config (Khởi tạo \& cấu hình)](#create--config-khởi-tạo--cấu-hình)
      - [.add\_node() (Thêm một bước xử lý)](#add_node-thêm-một-bước-xử-lý)
      - [START \& .add\_edge() \& END (Nối node A → B hoặc kết thúc)](#start--add_edge--end-nối-node-a--b-hoặc-kết-thúc)
    - [Display (Dùng để cung cấp thông tin)](#display-dùng-để-cung-cấp-thông-tin)
      - [.__dict__](#dict)
      - [.nodes (Xem thông tin các node)](#nodes-xem-thông-tin-các-node)
      - [.edges](#edges)
  - [.set\_entry\_point()](#set_entry_point)
  - [.add\_conditional\_edges()](#add_conditional_edges)
  - [.compile()](#compile)
  - [.invoke()](#invoke)
  - [.stream()](#stream)
---
# graph
## StateGraph (Tạo graph với state kiểu TypeDict)
**Syn**
```bash
from langgraph.graph import StateGraph

graph = StateGraph(StateType)

- Output: Object
```
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

workflow = StateGraph(AgentState)
print(workflow)
print(type(workflow))
# <langgraph.graph.state.StateGraph object at 0x739d718314b0>
# <class 'langgraph.graph.state.StateGraph'>
```
### Create & Config (Khởi tạo & cấu hình)
#### .add_node() (Thêm một bước xử lý)
**Syn**
```bash
graph.add_node("node_name", function)

- "node_name" = tên node
- function = hàm xử lý state
```
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

def print_ai_agent(state: AgentState):
    return state

workflow = StateGraph(AgentState)
workflow.add_node("print_ai_agent", print_ai_agent)

print(workflow.__dict__)
# {'nodes': {'print_ai_agent': StateNodeSpec(runnable=print_ai_agent(tags=None, recurse=True, explode_args=False, func_accepts={}), metadata=None, input_schema=<class '__main__.AgentState'>, retry_policy=None, cache_policy=None, ends=(), defer=False)}, 'edges': set(), 'branches': defaultdict(<class 'dict'>, {}), 'schemas': {<class '__main__.AgentState'>: {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x7d8806ebd640>, 'db': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd580>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7d8806ebcb00>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd600>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd6c0>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd5c0>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd680>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd700>}}, 'channels': {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x7d8806ebd640>, 'db': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd580>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7d8806ebcb00>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd600>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd6c0>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd5c0>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd680>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x7d8806ebd700>}, 'managed': {}, 'compiled': False, 'waiting_edges': set(), 'state_schema': <class '__main__.AgentState'>, 'input_schema': <class '__main__.AgentState'>, 'output_schema': <class '__main__.AgentState'>, 'context_schema': None}
```
#### START & .add_edge() & END (Nối node A → B hoặc kết thúc)
**Syn**
```bash
- graph.add_edge("node_a", "node_b")
- graph.add_edge("node_a", END)
```
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

def print_ai_agent(state: AgentState):
    return state

workflow = StateGraph(AgentState)
workflow.add_node("print_ai_agent", print_ai_agent)

workflow.add_edge(START, 'print_ai_agent')
workflow.add_edge("print_ai_agent", END)

print(workflow.__dict__)
# {'nodes': {'print_ai_agent': StateNodeSpec(runnable=print_ai_agent(tags=None, recurse=True, explode_args=False, func_accepts={}), metadata=None, input_schema=<class '__main__.AgentState'>, retry_policy=None, cache_policy=None, ends=(), defer=False)}, 'edges': {('print_ai_agent', '__end__'), ('__start__', 'print_ai_agent')}, 'branches': defaultdict(<class 'dict'>, {}), 'schemas': {<class '__main__.AgentState'>: {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x707497461500>, 'db': <langgraph.channels.last_value.LastValue object at 0x707497461440>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7074974609c0>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7074974614c0>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x707497461540>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x707497461480>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7074974615c0>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x707497461600>}}, 'channels': {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x707497461500>, 'db': <langgraph.channels.last_value.LastValue object at 0x707497461440>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7074974609c0>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7074974614c0>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x707497461540>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x707497461480>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7074974615c0>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x707497461600>}, 'managed': {}, 'compiled': False, 'waiting_edges': set(), 'state_schema': <class '__main__.AgentState'>, 'input_schema': <class '__main__.AgentState'>, 'output_schema': <class '__main__.AgentState'>, 'context_schema': None}
```
### Display (Dùng để cung cấp thông tin)
#### .__dict__
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

workflow = StateGraph(AgentState)
print(workflow.__dict__)
print(type(workflow))
# {'nodes': {}, 'edges': set(), 'branches': defaultdict(<class 'dict'>, {}), 'schemas': {<class '__main__.AgentState'>: {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x7b8d82265800>, 'db': <langgraph.channels.last_value.LastValue object at 0x7b8d82265740>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7b8d82264a00>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7b8d822657c0>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x7b8d82265840>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x7b8d82265780>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7b8d822658c0>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x7b8d82265900>}}, 'channels': {'messages': <langgraph.channels.binop.BinaryOperatorAggregate object at 0x7b8d82265800>, 'db': <langgraph.channels.last_value.LastValue object at 0x7b8d82265740>, 'current_user': <langgraph.channels.last_value.LastValue object at 0x7b8d82264a00>, 'llm': <langgraph.channels.last_value.LastValue object at 0x7b8d822657c0>, 'relevant_tools': <langgraph.channels.last_value.LastValue object at 0x7b8d82265840>, 'final_status': <langgraph.channels.last_value.LastValue object at 0x7b8d82265780>, 'final_message': <langgraph.channels.last_value.LastValue object at 0x7b8d822658c0>, 'action_id': <langgraph.channels.last_value.LastValue object at 0x7b8d82265900>}, 'managed': {}, 'compiled': False, 'waiting_edges': set(), 'state_schema': <class '__main__.AgentState'>, 'input_schema': <class '__main__.AgentState'>, 'output_schema': <class '__main__.AgentState'>, 'context_schema': None}
# <class 'langgraph.graph.state.StateGraph'>
```
#### .nodes (Xem thông tin các node)
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

def print_ai_agent(state: AgentState):
    return state

workflow = StateGraph(AgentState)
workflow.add_node("print_ai_agent", print_ai_agent)

print(workflow.nodes)
# {'print_ai_agent': StateNodeSpec(runnable=print_ai_agent(tags=None, recurse=True, explode_args=False, func_accepts={}), metadata=None, input_schema=<class '__main__.AgentState'>, retry_policy=None, cache_policy=None, ends=(), defer=False)}
```
#### .edges
**Ex**
```python
from langgraph.graph import StateGraph, START, END
from langgraph.graph.message import add_messages

from typing import Annotated, TypedDict, List, Dict, Any, Optional

from langchain_core.messages import SystemMessage, HumanMessage, AnyMessage

class AgentState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    db: Any
    current_user: Any
    llm: Any
    relevant_tools: List[Any]
    
    # Kết quả trả ra cuối cùng cho API
    final_status: Optional[str]
    final_message: Optional[str]
    action_id: Optional[str]

def print_ai_agent(state: AgentState):
    return state

workflow = StateGraph(AgentState)
workflow.add_node("print_ai_agent", print_ai_agent)

workflow.add_edge(START, 'print_ai_agent')
workflow.add_edge("print_ai_agent", END)

print(workflow.edges)
# {('print_ai_agent', '__end__'), ('__start__', 'print_ai_agent')}
```
## .set_entry_point()
```bash
Định nghĩa node bắt đầu
```
## .add_conditional_edges()
```bash
Cho phép rẽ nhánh / loop
```
**Syn**
```bash
graph.add_conditional_edges(
    "source_node",
    router_function
)
```
## .compile()
```bash
app = graph.compile()
```
## .invoke()
```bash
Chạy Graph
```
## .stream()
