- [Langchain Core Introduction](#langchain-core-introduction)
- [messages](#messages)
  - [SystemMessage](#systemmessage)
  - [HumanMessage() (Đại diện cho input của người dùng - user prompt)](#humanmessage-đại-diện-cho-input-của-người-dùng---user-prompt)
  - [Display (Dùng để cung cấp thông tin)](#display-dùng-để-cung-cấp-thông-tin)
    - [type](#type)
    - [.content](#content)
    - [.model\_dump() (chuyển từ object -\> dict)](#model_dump-chuyển-từ-object---dict)
- [PydanticOutputParser()](#pydanticoutputparser)
- [RunnableWithMessageHistory](#runnablewithmessagehistory)
- [RunnableLambda](#runnablelambda)
- [RunnableParallel](#runnableparallel)
- [PromptTemplate (Nhóm thiết lập khuôn mẫu)](#prompttemplate-nhóm-thiết-lập-khuôn-mẫu)
  - [.from\_template()](#from_template)
- [@tool (biến một python function thành một tool mà LLM/Agent có thể gọi)](#tool-biến-một-python-function-thành-một-tool-mà-llmagent-có-thể-gọi)
- [LangChain biến nó thành một StructuredTool](#langchain-biến-nó-thành-một-structuredtool)
- [runnables](#runnables)
  - [Runnable](#runnable)
- [ai\_msg](#ai_msg)
- [.bind\_tool()](#bind_tool)
---
# Langchain Core Introduction
```bash
- Nếu bạn thấy LangChain “khó đọc” vì nó chia theo pipeline, thì langchain_core chính là nơi định nghĩa các primitive (khối cơ bản) để pipeline đó hoạt động.
- Nói ngắn gọn: langchain_core không phải để build app trực tiếp, mà là để định nghĩa chuẩn chung cho các thành phần như model, prompt, output, chain.
```
# messages
**Ex2: Cách dùng chung với Chat Model**
```python
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")

messages = [
    SystemMessage(content="You are a strict Python teacher."),
    HumanMessage(content="Explain list comprehension.")
]

response = llm.invoke(messages)

print(response.content)

# Model sẽ đọc theo thứ tự: (có thể có thêm AIMessage nếu multi-turn)
# SystemMessage → hiểu vai trò
# HumanMessage → hiểu câu hỏi
# Sau đó sinh ra câu trả lời.
```
## SystemMessage
```bash
- Dùng để thiết lập “luật chơi” / ngữ cảnh chung cho model.
- Định nghĩa: vai trò, phong cách, quy tắc trả lời.
- Dùng khi muốn model:
    + trả lời theo phong cách cụ thể (giáo viên, chuyên gia…)
    + hạn chế/tuân thủ quy tắc
    + định hướng toàn bộ cuộc hội thoại
```
**Ex**
```python
from langchain_core.messages import SystemMessage

system_msg = SystemMessage(
    content="You are a helpful assistant that explains code clearly."
)
```
## HumanMessage() (Đại diện cho input của người dùng - user prompt)
```bash
HumanMessage không phải là dict, mà là một object (class). 
    Tuy nhiên, khi bạn print() nó, cách hiển thị có thể trông giống một dict, vì lớp này định nghĩa cách biểu diễn (__repr__) để dễ đọc.
```
**Ex**
```python
from langchain_core.messages import HumanMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)

print(human_msg) # content='Explain what a Python decorator is.' additional_kwargs={} response_metadata={}
```
## Display (Dùng để cung cấp thông tin)
### type
**Ex**
```python
from langchain_core.messages import HumanMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)

print(human_msg.type) # human
```
### .content
**Ex**
```python
from langchain_core.messages import HumanMessage, SystemMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)

print(human_msg.content) # Explain what a Python decorator is.
```
### .model_dump() (chuyển từ object -> dict)
**Ex**
```python
from langchain_core.messages import HumanMessage, SystemMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)

print(human_msg.model_dump())
# {'content': 'Explain what a Python decorator is.', 'additional_kwargs': {}, 'response_metadata': {}, 'type': 'human', 'name': None, 'id': None}
```
# PydanticOutputParser()
```bash
dùng khi muốn output chuẩn JSON
```
**Ex**
```bash
from pydantic import BaseModel
from langchain_core.output_parsers import PydanticOutputParser

class Answer(BaseModel):
    explanation: str
    example: str

parser = PydanticOutputParser(pydantic_object=Answer)

chain = prompt | model | parser
```
# RunnableWithMessageHistory
```bash
Dùng khi làm chatbot có session.
```
**Syn**
```bash
from langchain_core.runnables.history import RunnableWithMessageHistory
```
# RunnableLambda
```bash
Cho phép chèn hàm python vào pipeline
```
**Syn**
```bash
from langchain_core.runnables import RunnableLambda

def upper(text):
    return text.upper()

chain = prompt | model | RunnableLambda(upper)
```
# RunnableParallel
```bash
- Chạy song song
```
**Syn**
```bash
from langchain_core.runnables import RunnableParallel

chain = RunnableParallel(
    vi=prompt_vi | model,
    en=prompt_en | model
)

chain.invoke({"topic": "AI"})

# {
#   "vi": "...",
#   "en": "..."
# }
```
# PromptTemplate (Nhóm thiết lập khuôn mẫu)
```bash
- PromptTemplate là một template (khuôn mẫu) để tạo prompt động cho LLM
- Nó giống:
    + f-string trong Python
    + nhưng có cấu trúc + quản lý tốt hơn
- Dùng để làm gì?
    1. Truyền biến vào prompt. Thay vì viết cứng: "Hãy trả lời câu hỏi: AI là gì?". Bạn làm: "Hãy trả lời câu hỏi: {question}"
    2. Tái sử dụng prompt: Viết 1 lần. Dùng nhiều lần với dữ liệu khác nhau
    3. Build hệ thống LLM (RAG, chatbot, agent). Ví dụ:
        + {context} → dữ liệu từ vector DB
        + {question} → câu hỏi user
    4. Kết hợp với pipeline (|): prompt | llm
```
**Syn**
```bash
prompt = PromptTemplate(
    input_variables=["topic"],
    template="Giải thích {topic} trong 1 câu ngắn gọn"
)

- input_variables   : danh sách biến được phép truyền vào
```
**Ex**
```python
from langchain_community.chat_models import ChatOllama
from langchain_core.prompts import PromptTemplate

llm = ChatOllama(model="llama3", temperature=0)

prompt = PromptTemplate(
    input_variables=["topic"],
    template="Giải thích {topic} trong 1 câu ngắn gọn"
)

response = llm.invoke(prompt.format(topic="LangChain"))
print(response.content)
```
**Ex: Gợi ý nấu ăn**
```python
prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Bạn là trợ lý nấu ăn.
Nguyên liệu có sẵn: {ingredients}
Hãy gợi ý 1 món ăn phù hợp.
"""
)

llm.invoke(
    prompt.format(
        ingredients="trứng, cà chua, hành"
    )
)
```
**Ex3: PromptTemplate + dic**
```python
prompt.invoke({
    "ingredients": "trứng, cà chua"
})
```
**Ex: gợi ý tên món ăn**
```python
from langchain_community.chat_models import ChatOllama
from langchain_core.prompts import PromptTemplate

llm = ChatOllama(
    model="llama3",
    temperature=0
)

prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Bạn là backend AI cho ứng dụng Smart-Recipe.

Nhiệm vụ:
- CHỈ trả về TÊN MỘT MÓN ĂN DUY NHẤT
- KHÔNG mô tả
- KHÔNG liệt kê nguyên liệu
- KHÔNG hướng dẫn nấu
- KHÔNG thêm giải thích

Ràng buộc BẮT BUỘC:
- Chỉ đề xuất món ăn có thể chế biến từ TẤT CẢ nguyên liệu đã cho
- KHÔNG được bỏ qua nguyên liệu chính

Nguyên liệu chính: {ingredients}

Trả lời đúng 1 dòng, chỉ chứa tên món.
"""
)

response = llm.invoke(
    prompt.format(
        ingredients="thịt heo, hành tây, cà chua, mực"
    )
)

print(response.content)
```
## .from_template()
```bash
- Dùng để tạo một PromptTemplate từ chuỗi template
```
**Syn**
```bash
PromptTemplate.from_template(template_string)

- Input:
    + template_string: chuỗi có chứa biến {}
```
**Ex**
```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate.from_template(
    "Hãy trả lời câu hỏi: {question}"
)

# prompt = một object template. CHƯA có giá trị thật
# from_template = khai báo khuôn mẫu
```
# @tool (biến một python function thành một tool mà LLM/Agent có thể gọi)
```bash
Điểm quan trọng là: @tool(...) không phải để chạy function ngay. Nó là khai báo metadata + schema + function để LangChain biết tool này tên gì, nhận input gì và làm gì.
```
**Syn**
```bash
@tool(
    "get_user_info",
    args_schema=GetUserInfoInput
)

- Input:
    + "get_user_info": là tên của tool, LLM sẽ nhìn thấy tool với tên này
    + args_schema=GetUserInfoInput: nói với LangChain: Input của tool này phải tuân theo schema GetUserInfoInput.
**Ex1**
```python
def get_user_info():
    return "..."
# Đây chỉ là Python function

@tool("get_user_info", args_schema=GetUserInfoInput)
def get_user_info() -> str:
    ...
```
# LangChain biến nó thành một StructuredTool
# runnables
## Runnable
chưa trả lời câu hỏi nó dùng được trong các thư viện nào, có rất nhiều thư của langchain như là langchain_community, core, google_genai, ollama, openai, ... cơ mà

Đúng, câu hỏi của bạn là ainvoke() nằm ở đâu trong hệ sinh thái LangChain, và các package như langchain_core, langchain_google_genai, langchain_openai, langchain_ollama, langchain_community có dùng được nó không?

Câu trả lời quan trọng nhất là:

ainvoke() không thuộc riêng langchain_google_genai, langchain_openai, langchain_ollama hay langchain_community. Nó thuộc abstraction Runnable của langchain_core.

Các package khác cung cấp những implementation/model/tool/chain implement Runnable, nên chúng kế thừa/có API ainvoke().

1. Package nào thực sự định nghĩa ainvoke()?

Package cốt lõi là:

langchain_core

Cụ thể abstraction:

from langchain_core.runnables import Runnable

Runnable cung cấp một interface thống nhất, trong đó có các phương thức quan trọng như:

invoke()
ainvoke()
batch()
abatch()
stream()
astream()

Có thể hình dung:

                    langchain_core
                         │
                    Runnable
                         │
          ┌──────────────┼──────────────┐
          │              │              │
       invoke()       ainvoke()       stream()

Các package khác xây dựng object dựa trên abstraction này.

2. Vậy langchain_google_genai thì sao?

Ví dụ bạn đang dùng:

from langchain_google_genai import ChatGoogleGenerativeAI

Bạn tạo:

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash"
)

Object:

llm

là một Chat Model của LangChain và nằm trong hệ thống Runnable.

Vì vậy:

response = await llm.ainvoke(messages)

hoàn toàn hợp lệ.

Flow:

langchain_google_genai
        │
        │ ChatGoogleGenerativeAI
        ▼
   Chat Model
        │
        │ implements LangChain Runnable interface
        ▼
langchain_core
        │
        ▼
    .ainvoke()
3. langchain_openai

Tương tự:

from langchain_openai import ChatOpenAI
llm = ChatOpenAI(
    model="gpt-4o"
)

Có thể:

response = await llm.ainvoke(messages)

Không phải vì langchain_openai tự định nghĩa một kiểu ainvoke riêng.

Mà vì ChatOpenAI là một LangChain Runnable-compatible object.

4. langchain_ollama

Ví dụ:

from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="llama3.1"
)

Bạn cũng có:

response = await llm.ainvoke(messages)

Flow vẫn giống:

ChatOllama
    ↓
Runnable interface
    ↓
ainvoke()
5. langchain_community

Đây là chỗ dễ nhầm.

langchain_community không phải một loại Runnable khác.

Nó là package chứa nhiều integration/community implementations.

Ví dụ một số model, vector store, retriever, tools... nằm trong langchain_community.

Nếu một object cụ thể implement Runnable, thì bạn có thể dùng:

await object.ainvoke(...)

Nhưng không thể nói "mọi thứ trong langchain_community đều có ainvoke().

Đây là distinction rất quan trọng.

Ví dụ:

langchain_community
├── Model A        → có thể Runnable
├── Retriever B    → có thể Runnable
├── VectorStore C  → chưa chắc
├── Utility D      → chưa chắc
└── Tool E         → tùy interface

Cho nên không kiểm tra theo kiểu:

"Package này có ainvoke không?"

Mà phải hỏi:

"Object tôi đang sử dụng có implement Runnable không?"

6. langchain_core mới là "nền móng"

Bạn có thể hình dung toàn bộ ecosystem như này:

                         LangChain ecosystem
                                 │
                 ┌───────────────┴────────────────┐
                 │                                │
          langchain_core                    integrations
                 │                                │
          Runnable / Message               ┌──────┼──────┐
          Prompt / OutputParser             │      │      │
          Tool / Retriever              OpenAI Gemini Ollama
                 │
                 │ interface
                 ▼
             ainvoke()

Các integration:

langchain_openai
langchain_google_genai
langchain_ollama
langchain_community
...

cung cấp implementation.

langchain_core cung cấp abstraction/interface chung.

7. Package bạn đang có trong requirements

Bạn có:

langchain==1.2.7
langchain-classic==1.0.1
langchain-community==0.4.1
langchain-core==1.2.7
langchain-google-genai==4.2.1
langchain-ollama==1.0.1
langchain-openai==1.1.7
langchain-text-splitters==1.1.0
langgraph==1.0.7

Vai trò đại khái:

Package	Vai trò
langchain-core	Core abstraction, Runnable, messages, prompts, tools...
langchain	Framework/high-level LangChain
langchain-community	Community integrations
langchain-google-genai	Google Gemini integration
langchain-openai	OpenAI integration
langchain-ollama	Ollama integration
langchain-classic	API/implementation legacy
langchain-text-splitters	Text splitting
langgraph	Graph/stateful agent workflow

Trong số này, cái liên quan trực tiếp đến ainvoke() nhất là:

langchain-core
8. Cụ thể ChatGoogleGenerativeAI tại sao có ainvoke()?

Ví dụ:

from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(...)

Bạn không cần tự viết:

async def ainvoke(...):
    ...

Integration đã implement theo LangChain interface.

Vì vậy:

await llm.ainvoke(messages)

hoạt động.

Tương tự:

from langchain_openai import ChatOpenAI

llm = ChatOpenAI(...)
await llm.ainvoke(messages)

và:

from langchain_ollama import ChatOllama

llm = ChatOllama(...)
await llm.ainvoke(messages)

Cùng một interface:

                .ainvoke()
                   ▲
                   │
        ┌──────────┼──────────┐
        │          │          │
   Gemini       OpenAI      Ollama
        │          │          │
 ChatGoogle    ChatOpenAI  ChatOllama
 GenerativeAI

Điều này rất hay vì code Agent của bạn không cần biết model phía dưới là Gemini/OpenAI/Ollama.

9. Đây chính là lý do code của bạn dùng runnable

Bạn có code:

ai_msg = await runnable.ainvoke(invoke_messages)

thay vì:

if provider == "gemini":
    ...
elif provider == "openai":
    ...
elif provider == "ollama":
    ...

Đây là sức mạnh của abstraction.

Ví dụ:

if provider == "gemini":
    runnable = ChatGoogleGenerativeAI(...)

elif provider == "openai":
    runnable = ChatOpenAI(...)

elif provider == "ollama":
    runnable = ChatOllama(...)

Sau đó tất cả dùng chung:

ai_msg = await runnable.ainvoke(messages)

Agent không cần quan tâm implementation bên dưới.

10. Không chỉ LLM mới có ainvoke()

Đây là điểm bạn cần nhớ khi đọc LangChain code.

Ví dụ:

Chat Model
await llm.ainvoke(messages)
Prompt
await prompt.ainvoke(input)
Chain
chain = prompt | llm

await chain.ainvoke(input)
Parser
await parser.ainvoke(ai_message)
RunnableLambda
await runnable.ainvoke(input)
Retriever

Nhiều retriever trong LangChain cũng là Runnable:

docs = await retriever.ainvoke(query)
11. Ví dụ Retriever rất dễ thấy ý nghĩa

Giả sử:

retriever = vector_store.as_retriever()

Nếu retriever implement Runnable:

docs = await retriever.ainvoke(
    "Python async là gì?"
)

Input:

str

Output:

list[Document]

Tức là:

"Python async là gì?"
          │
          ▼
     retriever
          │
       ainvoke()
          │
          ▼
[
    Document(...),
    Document(...),
    Document(...)
]

Không phải LLM nhưng vẫn dùng .ainvoke().

12. Prompt cũng có thể là Runnable

Ví dụ:

from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_messages([
    ("system", "Bạn là trợ lý AI."),
    ("human", "{question}")
])

Sau đó:

result = await prompt.ainvoke({
    "question": "Python là gì?"
})

Prompt nhận:

dict

và trả ra một prompt/message representation.

Sau đó:

chain = prompt | llm

thì:

result = await chain.ainvoke({
    "question": "Python là gì?"
})
13. | cũng liên quan trực tiếp đến Runnable

Bạn sẽ thấy rất nhiều code LangChain:

chain = prompt | llm | parser

Đây không phải pipe của Linux.

Nó là Runnable composition.

input
  │
  ▼
┌────────┐
│ prompt │
└───┬────┘
    │
    ▼
┌────────┐
│  llm   │
└───┬────┘
    │
    ▼
┌────────┐
│ parser │
└───┬────┘
    │
    ▼
 output

Và toàn bộ:

prompt | llm | parser

trở thành một Runnable.

Vì vậy:

result = await chain.ainvoke(input)
14. Vậy ainvoke() có dùng được với langgraph không?

Có, nhưng cần phân biệt.

LangGraph node của bạn:

async def agent_node(state):
    ...

không phải cứ là LangGraph node thì tự động gọi ainvoke().

Trong node bạn chủ động gọi:

ai_msg = await runnable.ainvoke(messages)

LangGraph đang điều phối workflow, còn Runnable đang thực thi model/chain.

Architecture:

                 LangGraph
                     │
                 agent_node
                     │
                     ▼
              LangChain Runnable
                     │
               .ainvoke()
                     │
             ┌───────┼───────┐
             ▼       ▼       ▼
           Gemini  OpenAI   Ollama

Đây chính là architecture code của bạn đang dùng.

15. Còn langchain_google_genai có tự định nghĩa ainvoke không?

Về mặt tư duy sử dụng API, đừng hiểu nó là mỗi integration có một ainvoke() riêng.

Hãy hiểu:

langchain_core
    ↓
định nghĩa Runnable contract
    ↓
integration implement contract

Ví dụ:

ChatGoogleGenerativeAI ─┐
ChatOpenAI              ├──→ Runnable → ainvoke()
ChatOllama               │
SomeCommunityModel ─────┘

Nên Agent code có tính portable.

16. Một cách kiểm tra ngay trong Python

Bạn có thể kiểm tra object của mình:

from langchain_core.runnables import Runnable

print(isinstance(runnable, Runnable))

Nếu:

True

thì bạn đang làm việc với Runnable.

Hoặc:

print(type(runnable))
print(hasattr(runnable, "ainvoke"))

Ví dụ:

<class 'langchain_google_genai.chat_models.ChatGoogleGenerativeAI'>
True
17. Nhưng đừng hiểu "có ainvoke" = "mọi package đều có"

Ví dụ bạn import:

from langchain_core.documents import Document

Document không phải Runnable.

Bạn không thể làm:

await document.ainvoke(...)

Tương tự một object tiện ích bất kỳ trong langchain_community cũng không nhất thiết có.

Cho nên quy tắc chính xác là:

Không phân loại theo package. Phân loại theo object/interface.

18. Bảng tổng kết cho đúng với câu hỏi của bạn
Thứ	Package thường gặp	Có .ainvoke()?
Runnable	langchain_core	✅
ChatGoogleGenerativeAI	langchain_google_genai	✅
ChatOpenAI	langchain_openai	✅
ChatOllama	langchain_ollama	✅
Chain prompt | llm	langchain_core	✅
RunnableLambda	langchain_core	✅
Nhiều Retriever	langchain_core / integration	✅
Một số Tools	tùy implementation	Có thể
Document	langchain_core	❌
AIMessage	langchain_core	❌ — nó là data/message, không phải Runnable
AgentState của bạn	code riêng	❌
LangGraph StateGraph	langgraph	Không phải cách gọi node bằng .ainvoke() theo nghĩa Runnable model
Cách nhớ ngắn gọn nhất

Bạn đang có 3 tầng:

┌──────────────────────────────────────────┐
│              LANGGRAPH                   │
│  workflow / state / node / edge          │
│                                          │
│              agent_node                  │
│                   │                      │
└───────────────────┼──────────────────────┘
                    ▼
┌──────────────────────────────────────────┐
│           LANGCHAIN CORE                 │
│                                          │
│              Runnable                    │
│                 │                        │
│              ainvoke()                   │
└───────────────────┼──────────────────────┘
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       Gemini     OpenAI     Ollama
       package    package    package

langchain_core định nghĩa abstraction; langchain_google_genai, langchain_openai, langchain_ollama, nhiều integration trong langchain_community cung cấp implementation phù hợp với abstraction đó.

Vì vậy trong code của bạn:

ai_msg = await runnable.ainvoke(invoke_messages)

thứ quyết định input/output cụ thể là gì không phải tên ainvoke(), mà là runnable đang chứa object nào. Đây là điểm quan trọng nhất để đọc tiếp agent_node của bạn.

Đúng, câu hỏi của bạn là ainvoke() nằm ở đâu trong hệ sinh thái LangChain, và các package như langchain_core, langchain_google_genai, langchain_openai, langchain_ollama, langchain_community có dùng được nó không?

Câu trả lời quan trọng nhất là:

ainvoke() không thuộc riêng langchain_google_genai, langchain_openai, langchain_ollama hay langchain_community. Nó thuộc abstraction Runnable của langchain_core.

Các package khác cung cấp những implementation/model/tool/chain implement Runnable, nên chúng kế thừa/có API ainvoke().

1. Package nào thực sự định nghĩa ainvoke()?

Package cốt lõi là:

langchain_core

Cụ thể abstraction:

from langchain_core.runnables import Runnable

Runnable cung cấp một interface thống nhất, trong đó có các phương thức quan trọng như:

invoke()
ainvoke()
batch()
abatch()
stream()
astream()

Có thể hình dung:

                    langchain_core
                         │
                    Runnable
                         │
          ┌──────────────┼──────────────┐
          │              │              │
       invoke()       ainvoke()       stream()

Các package khác xây dựng object dựa trên abstraction này.

2. Vậy langchain_google_genai thì sao?

Ví dụ bạn đang dùng:

from langchain_google_genai import ChatGoogleGenerativeAI

Bạn tạo:

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash"
)

Object:

llm

là một Chat Model của LangChain và nằm trong hệ thống Runnable.

Vì vậy:

response = await llm.ainvoke(messages)

hoàn toàn hợp lệ.

Flow:

langchain_google_genai
        │
        │ ChatGoogleGenerativeAI
        ▼
   Chat Model
        │
        │ implements LangChain Runnable interface
        ▼
langchain_core
        │
        ▼
    .ainvoke()
3. langchain_openai

Tương tự:

from langchain_openai import ChatOpenAI
llm = ChatOpenAI(
    model="gpt-4o"
)

Có thể:

response = await llm.ainvoke(messages)

Không phải vì langchain_openai tự định nghĩa một kiểu ainvoke riêng.

Mà vì ChatOpenAI là một LangChain Runnable-compatible object.

4. langchain_ollama

Ví dụ:

from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="llama3.1"
)

Bạn cũng có:

response = await llm.ainvoke(messages)

Flow vẫn giống:

ChatOllama
    ↓
Runnable interface
    ↓
ainvoke()
5. langchain_community

Đây là chỗ dễ nhầm.

langchain_community không phải một loại Runnable khác.

Nó là package chứa nhiều integration/community implementations.

Ví dụ một số model, vector store, retriever, tools... nằm trong langchain_community.

Nếu một object cụ thể implement Runnable, thì bạn có thể dùng:

await object.ainvoke(...)

Nhưng không thể nói "mọi thứ trong langchain_community đều có ainvoke().

Đây là distinction rất quan trọng.

Ví dụ:

langchain_community
├── Model A        → có thể Runnable
├── Retriever B    → có thể Runnable
├── VectorStore C  → chưa chắc
├── Utility D      → chưa chắc
└── Tool E         → tùy interface

Cho nên không kiểm tra theo kiểu:

"Package này có ainvoke không?"

Mà phải hỏi:

"Object tôi đang sử dụng có implement Runnable không?"

6. langchain_core mới là "nền móng"

Bạn có thể hình dung toàn bộ ecosystem như này:

                         LangChain ecosystem
                                 │
                 ┌───────────────┴────────────────┐
                 │                                │
          langchain_core                    integrations
                 │                                │
          Runnable / Message               ┌──────┼──────┐
          Prompt / OutputParser             │      │      │
          Tool / Retriever              OpenAI Gemini Ollama
                 │
                 │ interface
                 ▼
             ainvoke()

Các integration:

langchain_openai
langchain_google_genai
langchain_ollama
langchain_community
...

cung cấp implementation.

langchain_core cung cấp abstraction/interface chung.

7. Package bạn đang có trong requirements

Bạn có:

langchain==1.2.7
langchain-classic==1.0.1
langchain-community==0.4.1
langchain-core==1.2.7
langchain-google-genai==4.2.1
langchain-ollama==1.0.1
langchain-openai==1.1.7
langchain-text-splitters==1.1.0
langgraph==1.0.7

Vai trò đại khái:

Package	Vai trò
langchain-core	Core abstraction, Runnable, messages, prompts, tools...
langchain	Framework/high-level LangChain
langchain-community	Community integrations
langchain-google-genai	Google Gemini integration
langchain-openai	OpenAI integration
langchain-ollama	Ollama integration
langchain-classic	API/implementation legacy
langchain-text-splitters	Text splitting
langgraph	Graph/stateful agent workflow

Trong số này, cái liên quan trực tiếp đến ainvoke() nhất là:

langchain-core
8. Cụ thể ChatGoogleGenerativeAI tại sao có ainvoke()?

Ví dụ:

from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(...)

Bạn không cần tự viết:

async def ainvoke(...):
    ...

Integration đã implement theo LangChain interface.

Vì vậy:

await llm.ainvoke(messages)

hoạt động.

Tương tự:

from langchain_openai import ChatOpenAI

llm = ChatOpenAI(...)
await llm.ainvoke(messages)

và:

from langchain_ollama import ChatOllama

llm = ChatOllama(...)
await llm.ainvoke(messages)

Cùng một interface:

                .ainvoke()
                   ▲
                   │
        ┌──────────┼──────────┐
        │          │          │
   Gemini       OpenAI      Ollama
        │          │          │
 ChatGoogle    ChatOpenAI  ChatOllama
 GenerativeAI

Điều này rất hay vì code Agent của bạn không cần biết model phía dưới là Gemini/OpenAI/Ollama.

9. Đây chính là lý do code của bạn dùng runnable

Bạn có code:

ai_msg = await runnable.ainvoke(invoke_messages)

thay vì:

if provider == "gemini":
    ...
elif provider == "openai":
    ...
elif provider == "ollama":
    ...

Đây là sức mạnh của abstraction.

Ví dụ:

if provider == "gemini":
    runnable = ChatGoogleGenerativeAI(...)

elif provider == "openai":
    runnable = ChatOpenAI(...)

elif provider == "ollama":
    runnable = ChatOllama(...)

Sau đó tất cả dùng chung:

ai_msg = await runnable.ainvoke(messages)

Agent không cần quan tâm implementation bên dưới.

10. Không chỉ LLM mới có ainvoke()

Đây là điểm bạn cần nhớ khi đọc LangChain code.

Ví dụ:

Chat Model
await llm.ainvoke(messages)
Prompt
await prompt.ainvoke(input)
Chain
chain = prompt | llm

await chain.ainvoke(input)
Parser
await parser.ainvoke(ai_message)
RunnableLambda
await runnable.ainvoke(input)
Retriever

Nhiều retriever trong LangChain cũng là Runnable:

docs = await retriever.ainvoke(query)
11. Ví dụ Retriever rất dễ thấy ý nghĩa

Giả sử:

retriever = vector_store.as_retriever()

Nếu retriever implement Runnable:

docs = await retriever.ainvoke(
    "Python async là gì?"
)

Input:

str

Output:

list[Document]

Tức là:

"Python async là gì?"
          │
          ▼
     retriever
          │
       ainvoke()
          │
          ▼
[
    Document(...),
    Document(...),
    Document(...)
]

Không phải LLM nhưng vẫn dùng .ainvoke().

12. Prompt cũng có thể là Runnable

Ví dụ:

from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_messages([
    ("system", "Bạn là trợ lý AI."),
    ("human", "{question}")
])

Sau đó:

result = await prompt.ainvoke({
    "question": "Python là gì?"
})

Prompt nhận:

dict

và trả ra một prompt/message representation.

Sau đó:

chain = prompt | llm

thì:

result = await chain.ainvoke({
    "question": "Python là gì?"
})
13. | cũng liên quan trực tiếp đến Runnable

Bạn sẽ thấy rất nhiều code LangChain:

chain = prompt | llm | parser

Đây không phải pipe của Linux.

Nó là Runnable composition.

input
  │
  ▼
┌────────┐
│ prompt │
└───┬────┘
    │
    ▼
┌────────┐
│  llm   │
└───┬────┘
    │
    ▼
┌────────┐
│ parser │
└───┬────┘
    │
    ▼
 output

Và toàn bộ:

prompt | llm | parser

trở thành một Runnable.

Vì vậy:

result = await chain.ainvoke(input)
14. Vậy ainvoke() có dùng được với langgraph không?

Có, nhưng cần phân biệt.

LangGraph node của bạn:

async def agent_node(state):
    ...

không phải cứ là LangGraph node thì tự động gọi ainvoke().

Trong node bạn chủ động gọi:

ai_msg = await runnable.ainvoke(messages)

LangGraph đang điều phối workflow, còn Runnable đang thực thi model/chain.

Architecture:

                 LangGraph
                     │
                 agent_node
                     │
                     ▼
              LangChain Runnable
                     │
               .ainvoke()
                     │
             ┌───────┼───────┐
             ▼       ▼       ▼
           Gemini  OpenAI   Ollama

Đây chính là architecture code của bạn đang dùng.

15. Còn langchain_google_genai có tự định nghĩa ainvoke không?

Về mặt tư duy sử dụng API, đừng hiểu nó là mỗi integration có một ainvoke() riêng.

Hãy hiểu:

langchain_core
    ↓
định nghĩa Runnable contract
    ↓
integration implement contract

Ví dụ:

ChatGoogleGenerativeAI ─┐
ChatOpenAI              ├──→ Runnable → ainvoke()
ChatOllama               │
SomeCommunityModel ─────┘

Nên Agent code có tính portable.

16. Một cách kiểm tra ngay trong Python

Bạn có thể kiểm tra object của mình:

from langchain_core.runnables import Runnable

print(isinstance(runnable, Runnable))

Nếu:

True

thì bạn đang làm việc với Runnable.

Hoặc:

print(type(runnable))
print(hasattr(runnable, "ainvoke"))

Ví dụ:

<class 'langchain_google_genai.chat_models.ChatGoogleGenerativeAI'>
True
17. Nhưng đừng hiểu "có ainvoke" = "mọi package đều có"

Ví dụ bạn import:

from langchain_core.documents import Document

Document không phải Runnable.

Bạn không thể làm:

await document.ainvoke(...)

Tương tự một object tiện ích bất kỳ trong langchain_community cũng không nhất thiết có.

Cho nên quy tắc chính xác là:

Không phân loại theo package. Phân loại theo object/interface.

18. Bảng tổng kết cho đúng với câu hỏi của bạn
Thứ	Package thường gặp	Có .ainvoke()?
Runnable	langchain_core	✅
ChatGoogleGenerativeAI	langchain_google_genai	✅
ChatOpenAI	langchain_openai	✅
ChatOllama	langchain_ollama	✅
Chain prompt | llm	langchain_core	✅
RunnableLambda	langchain_core	✅
Nhiều Retriever	langchain_core / integration	✅
Một số Tools	tùy implementation	Có thể
Document	langchain_core	❌
AIMessage	langchain_core	❌ — nó là data/message, không phải Runnable
AgentState của bạn	code riêng	❌
LangGraph StateGraph	langgraph	Không phải cách gọi node bằng .ainvoke() theo nghĩa Runnable model
Cách nhớ ngắn gọn nhất

Bạn đang có 3 tầng:

┌──────────────────────────────────────────┐
│              LANGGRAPH                   │
│  workflow / state / node / edge          │
│                                          │
│              agent_node                  │
│                   │                      │
└───────────────────┼──────────────────────┘
                    ▼
┌──────────────────────────────────────────┐
│           LANGCHAIN CORE                 │
│                                          │
│              Runnable                    │
│                 │                        │
│              ainvoke()                   │
└───────────────────┼──────────────────────┘
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       Gemini     OpenAI     Ollama
       package    package    package

langchain_core định nghĩa abstraction; langchain_google_genai, langchain_openai, langchain_ollama, nhiều integration trong langchain_community cung cấp implementation phù hợp với abstraction đó.

Vì vậy trong code của bạn:

ai_msg = await runnable.ainvoke(invoke_messages)

thứ quyết định input/output cụ thể là gì không phải tên ainvoke(), mà là runnable đang chứa object nào. Đây là điểm quan trọng nhất để đọc tiếp agent_node của bạn.

Được. Với dòng code bạn đang gặp:

ai_msg = await runnable.ainvoke(invoke_messages)

thì ainvoke() là một trong những API quan trọng nhất của LangChain Runnable. Nếu hiểu Runnable và ainvoke() thì bạn sẽ hiểu được khá nhiều đoạn code LangChain/LangGraph.

1. ainvoke() là gì?

Hiểu đơn giản:

await runnable.ainvoke(input)

có nghĩa là:

Chạy runnable một cách bất đồng bộ (async) với input, rồi lấy kết quả trả về.

Có thể hình dung:

input
  │
  ▼
┌─────────────────┐
│    runnable     │
│                 │
│ model / chain / │
│ parser / ...    │
└─────────────────┘
  │
  ▼
output

Ví dụ:

result = await runnable.ainvoke("Hello")

Ở đây:

runnable = thứ cần được thực thi
"Hello" = input
result = output
2. Phân tích cú pháp dòng code của bạn

Bạn có:

ai_msg = await runnable.ainvoke(invoke_messages)

Tách ra:

ai_msg
  =
await
  runnable
      .
    ainvoke
       (
     invoke_messages
       )
runnable

Là object có interface Runnable.

Ví dụ có thể là:

llm

hoặc:

llm.bind_tools(tools)

hoặc:

prompt | llm

hoặc:

prompt | llm | parser
.ainvoke(...)

Gọi phương thức async của Runnable.

runnable.ainvoke(...)
invoke_messages

Là input truyền vào Runnable.

Nó có thể là:

str

hoặc:

dict

hoặc:

list

tùy runnable đang là cái gì.

await

Vì ainvoke() là async nên nó trả về một awaitable/coroutine.

result = runnable.ainvoke(input)

chưa phải kết quả cuối.

Phải:

result = await runnable.ainvoke(input)

thì mới lấy được output.

3. invoke() và ainvoke() khác nhau thế nào?

LangChain thường có cặp:

invoke()
ainvoke()

Ví dụ synchronous:

result = runnable.invoke(input)

và asynchronous:

result = await runnable.ainvoke(input)

Có thể hiểu:

invoke()
   ↓
chạy synchronous
   ↓
output


ainvoke()
   ↓
chạy asynchronous
   ↓
await
   ↓
output

Trong FastAPI/LangGraph async code của bạn, thường sẽ thấy:

async def agent_node(state):
    ...
    ai_msg = await runnable.ainvoke(messages)

vì toàn bộ workflow đang chạy async.

4. Runnable là gì?

Đây mới là khái niệm quan trọng.

Trong LangChain, rất nhiều thành phần được chuẩn hóa thành:

Runnable

Nói đơn giản:

Một Runnable là một object có thể nhận input → xử lý → trả output.

Ví dụ:

Prompt
  ↓
LLM
  ↓
Parser

có thể tạo thành:

chain = prompt | llm | parser

Toàn bộ chain này cũng là một Runnable.

Vì vậy bạn có thể:

result = await chain.ainvoke(input)
5. ainvoke() dùng được cho những gì?

Không phải chỉ LLM.

Đây là điểm rất quan trọng.

ainvoke() có thể dùng với bất kỳ LangChain object nào implement Runnable interface.

Ví dụ:

Chat model
await llm.ainvoke(...)
Prompt
await prompt.ainvoke(...)
Chain
await chain.ainvoke(...)
Output parser
await parser.ainvoke(...)
RunnableLambda
await runnable_lambda.ainvoke(...)
RunnablePassthrough
await RunnablePassthrough().ainvoke(...)
RunnableSequence
await sequence.ainvoke(...)
LLM có bind tools
runnable = llm.bind_tools(tools)

result = await runnable.ainvoke(messages)
6. Điều quan trọng: input/output không cố định

Đây là chỗ dễ nhầm nhất.

Không thể nói:

"ainvoke() nhận List[Message] và trả AIMessage."

Không đúng trong mọi trường hợp.

ainvoke() có input/output phụ thuộc vào Runnable cụ thể.

Ví dụ:

Runnable A
input: str
output: str

Runnable B
input: dict
output: AIMessage

Runnable C
input: list[BaseMessage]
output: AIMessage

Runnable D
input: str
output: MyPydanticModel
7. Ví dụ 1 — LLM nhận messages

Đây gần nhất với code của bạn.

Ví dụ:

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.messages import HumanMessage

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash"
)

messages = [
    HumanMessage(content="Thủ đô Việt Nam là gì?")
]

ai_msg = await llm.ainvoke(messages)

Input:

messages

có kiểu:

list[BaseMessage]

thực tế:

[
    HumanMessage(...)
]

Output thường là:

AIMessage

Ví dụ conceptually:

AIMessage(
    content="Thủ đô Việt Nam là Hà Nội."
)
8. ai_msg của bạn thực chất là gì?

Trong code của bạn:

ai_msg = await runnable.ainvoke(invoke_messages)

nếu:

runnable = llm.bind_tools(tools)

thì rất có khả năng:

invoke_messages

là:

list[BaseMessage]

và:

ai_msg

là:

AIMessage

Ví dụ:

print(type(invoke_messages))

có thể:

<class 'list'>

và:

print(type(invoke_messages[0]))

có thể:

<class 'langchain_core.messages.human.HumanMessage'>

Còn:

print(type(ai_msg))

thường:

<class 'langchain_core.messages.ai.AIMessage'>
9. AIMessage không chỉ chứa text

Đây là điểm cực kỳ quan trọng đối với Agent của bạn.

Bạn có thể tưởng tượng:

ai_msg = AIMessage(
    content="Tôi sẽ kiểm tra email của bạn.",
)

Nhưng khi LLM quyết định gọi tool, nó có thể trả:

AIMessage(
    content="",
    tool_calls=[
        {
            "name": "get_user_email",
            "args": {},
            "id": "call_123"
        }
    ]
)

Do đó Agent của bạn có thể kiểm tra:

ai_msg.tool_calls

và thấy:

[
    {
        "name": "get_user_email",
        "args": {},
        "id": "call_123"
    }
]

Đây chính là cách:

User
 ↓
Agent LLM
 ↓
ainvoke()
 ↓
AIMessage
 ↓
tool_calls?
 ├── không → final answer
 │
 └── có → execute tool
10. Ví dụ 2 — RunnableLambda

Không cần LLM.

from langchain_core.runnables import RunnableLambda

runnable = RunnableLambda(lambda x: x * 2)

result = await runnable.ainvoke(10)

print(result)

Output:

20

Input:

10

kiểu:

int

Output:

20

kiểu:

int

Điều này chứng minh:

ainvoke() không phải API chỉ dành cho AI model.

Nó là API của Runnable abstraction.

11. Ví dụ 3 — Input là dict
from langchain_core.runnables import RunnableLambda

runnable = RunnableLambda(
    lambda x: f"Xin chào {x['name']}"
)

result = await runnable.ainvoke({
    "name": "Thắng"
})

Input:

dict

Output:

"Xin chào Thắng"

kiểu:

str
12. Ví dụ 4 — Prompt → LLM

Đây mới là thứ bạn sẽ gặp rất nhiều.

prompt = ChatPromptTemplate.from_messages([
    ("system", "Bạn là trợ lý AI."),
    ("human", "{question}")
])

chain = prompt | llm

Ở đây:

prompt
  ↓
llm

chain là một Runnable.

Sau đó:

response = await chain.ainvoke({
    "question": "Python là gì?"
})

Input:

{
    "question": "Python là gì?"
}

Output:

AIMessage
13. Tại sao prompt | llm lại chạy được?

LangChain sử dụng Runnable composition.

chain = prompt | llm

nghĩa conceptually:

input
  ↓
Prompt
  ↓
formatted messages
  ↓
LLM
  ↓
AIMessage

Sau đó:

await chain.ainvoke(input)

LangChain tự truyền output của bước trước thành input cho bước sau.

14. Có thể nối tiếp parser

Ví dụ:

chain = prompt | llm | parser

thì:

input
 ↓
prompt
 ↓
LLM
 ↓
AIMessage
 ↓
parser
 ↓
parsed result

Khi đó:

result = await chain.ainvoke(input)

output không còn nhất thiết là AIMessage.

Nó có thể là:

dict

hoặc:

Pydantic model

tùy parser.

15. So sánh invoke, ainvoke, stream, astream

Bạn nên nhớ 4 API này:

API	Async?	Streaming?	Ý nghĩa
invoke()	❌	❌	chạy một lần
ainvoke()	✅	❌	chạy async một lần
stream()	❌	✅	stream output
astream()	✅	✅	async stream

Ví dụ:

result = runnable.invoke(input)

vs:

result = await runnable.ainvoke(input)

vs:

for chunk in runnable.stream(input):
    ...

vs:

async for chunk in runnable.astream(input):
    ...
16. ainvoke() và SSE trong project của bạn

Hai thứ này cũng cần phân biệt.

Bạn đang có:

LangGraph
   ↓
agent_node
   ↓
LLM
   ↓
ainvoke()

ainvoke() không phải SSE.

Ví dụ:

ai_msg = await runnable.ainvoke(messages)

chỉ có nghĩa:

Backend gọi model/chain async và chờ kết quả.

Còn SSE:

Backend
   │
   │ event
   ▼
Browser

là cơ chế đẩy progress/event từ backend xuống frontend.

Hai thứ có thể kết hợp:

Frontend
   ↑
   │ SSE
   │
FastAPI
   │
   ▼
LangGraph
   │
   ▼
agent_node
   │
   ▼
await runnable.ainvoke(...)
   │
   ▼
AIMessage
17. Quay lại chính code Agent của bạn

Giả sử code là:

tools = state.get("active_tools") or []

runnable = llm.bind_tools(tools)

invoke_messages = state["messages"]

ai_msg = await runnable.ainvoke(invoke_messages)

Ta có flow:

Bước 1
tools = state["active_tools"]

Ví dụ:

[
    get_user_email,
    get_user_profile
]
Bước 2
runnable = llm.bind_tools(tools)

Tạo một Runnable LLM đã biết:

LLM có thể sử dụng:
- get_user_email
- get_user_profile
Bước 3
invoke_messages = state["messages"]

Ví dụ:

[
    HumanMessage(
        content="Email của tôi là gì?"
    )
]
Bước 4
ai_msg = await runnable.ainvoke(invoke_messages)

LLM nhận:

messages
+
tool definitions

và suy luận.

Có thể trả:

AIMessage(
    content="",
    tool_calls=[
        {
            "name": "get_user_email",
            "args": {},
            "id": "abc123"
        }
    ]
)
18. Sau ainvoke() thì Agent làm gì?

Đây chính là chỗ bạn đang học trong agent_node.

Conceptually:

ai_msg = await runnable.ainvoke(invoke_messages)

if ai_msg.tool_calls:
    # LLM muốn gọi tool
    ...
else:
    # LLM không muốn gọi tool
    # → có thể final answer
    ...

Graph của bạn có thể trở thành:

                  active_tools
                       ↓
                    bind_tools
                       ↓
messages ───────→ LLM Runnable
                       │
                 await ainvoke()
                       │
                       ▼
                   AIMessage
                    /      \
                   /        \
            tool_calls?     no tool_calls
                │                │
                ▼                ▼
             execute          final/evaluate
                │
                ▼
            ToolMessage
                │
                ▼
              Agent

Đây là một trong những flow cốt lõi của Agentic workflow.

19. Một cách kiểm tra cực tốt khi đọc code

Khi gặp:

result = await something.ainvoke(input)

đừng cố nhớ ngay output là gì.

Hãy truy ngược:

Câu hỏi 1
something

là object gì?

Ví dụ:

something = llm

→ ChatModel.

Hoặc:

something = prompt | llm

→ RunnableSequence.

Hoặc:

something = llm.bind_tools(tools)

→ Runnable ChatModel đã bind tools.

Câu hỏi 2

Input là gì?

input

Ví dụ:

str

hay:

dict

hay:

list[BaseMessage]
Câu hỏi 3

Output của Runnable đó là gì?

Ví dụ:

ChatModel
    input: messages
    output: AIMessage

hoặc:

RunnableLambda
    input: int
    output: int
20. Công thức tổng quát bạn nên nhớ
output = await runnable.ainvoke(input)

có thể đọc thành:

"Hãy chạy Runnable này một cách bất đồng bộ với input này, đợi nó hoàn thành, rồi lấy output."

Và:

                    Runnable
                       │
             ┌─────────┴─────────┐
             │                   │
          Input                Output
             │                   │
          tùy loại             tùy loại

Không có một kiểu input/output cố định cho ainvoke().

Với chính Agent của bạn

Dòng:

ai_msg = await runnable.ainvoke(invoke_messages)

nên đọc thành:

invoke_messages
      │
      │ list[BaseMessage]
      ▼
runnable = LLM + active_tools
      │
      │ await ainvoke()
      ▼
ai_msg
      │
      │ AIMessage
      ├───────────────┐
      │               │
      ▼               ▼
tool_calls       final content
      │
      ▼
execute tool

Điểm mấu chốt: ainvoke() không phải "hàm gọi AI" riêng biệt. Nó là interface async chung của LangChain Runnable. Model, prompt, chain, parser, lambda, tool-bound model... nếu implement Runnable thì đều có thể dùng .ainvoke(); kiểu input/output phụ thuộc vào Runnable cụ thể.

# .bind_tool() 

Bạn có thể hiểu:

from langchain_core.language_models import BaseChatModel

BaseChatModel là abstraction cho các Chat Model.

Các integration package sau đó triển khai nó:

                    langchain_core
                         │
                    BaseChatModel
                         │
          ┌──────────────┼───────────────┐
          ▼              ▼               ▼
     ChatOllama      ChatOpenAI    ChatGoogleGenerativeAI
          │              │               │
          ▼              ▼               ▼
       Ollama          OpenAI           Gemini
2. Vậy ChatOllama.bind_tools() là gì?

Khi bạn viết:

from langchain_ollama import ChatOllama

llm = ChatOllama(model="llama3")

llm_with_tools = llm.bind_tools(tools)

thì:

llm
│
│ ChatOllama object
│
└── bind_tools(tools)
          │
          ▼
    Runnable / ChatModel
    đã được cấu hình tool

bind_tools() không phải API của Ollama theo nghĩa:

ollama.bind_tools(...)

Mà đây là LangChain abstraction, sau đó ChatOllama chuyển thông tin tools sang format mà Ollama/model backend hiểu được.

3. Đây chính là ý bạn nói "abstract lại"

Bạn nói:

"mấy cái kiểu langchain_ollama chỉ abstract lại"

Gần đúng, nhưng nên nói chính xác hơn:

langchain_ollama là integration/implementation layer. Nó implement các abstraction/interface của langchain_core để LangChain có thể sử dụng Ollama theo một API thống nhất.

Ví dụ:

                  LANGCHAIN CORE
                       │
                       │ định nghĩa abstraction
                       ▼
                BaseChatModel
                       │
             ┌─────────┼──────────┐
             │         │          │
             ▼         ▼          ▼
       ChatOllama  ChatOpenAI  ChatGoogle
             │         │          │
             ▼         ▼          ▼
          Ollama    OpenAI      Gemini

Do đó application code của bạn có thể viết:

llm.bind_tools(tools)

mà không cần tự viết:

ollama_api.bind_tools(...)
openai_api.bind_tools(...)
gemini_api.bind_tools(...)
4. Nhưng có một nuance rất quan trọng

Không phải mọi model LangChain đều đảm bảo hỗ trợ tool calling.

Ví dụ về mặt interface:

llm.bind_tools(tools)

có thể tồn tại.

Nhưng backend/model cụ thể có thể:

hỗ trợ native tool calling;
hỗ trợ một phần;
hoặc không hỗ trợ.

Vì vậy có hai tầng:

Tầng LangChain
    │
    │ "Tôi muốn bind các tools này"
    ▼
bind_tools(...)
    │
    ▼
Integration
    │
    │ chuyển đổi tools sang format của provider
    ▼
Provider API
    │
    ▼
Model
5. bind_tools() thực chất làm gì?

Ví dụ bạn có tool:

@tool
def search_customer(customer_id: int):
    ...

Sau đó:

llm_with_tools = llm.bind_tools([search_customer])

Nó không chạy search_customer() ngay.

Đây là điểm cực kỳ quan trọng.

Nó chỉ nói với model:

"Trong quá trình trả lời, model có quyền yêu cầu gọi tool này."

Sau đó:

response = await llm_with_tools.ainvoke(messages)

Model có thể trả:

AIMessage
   │
   ├── content = ""
   │
   └── tool_calls
          │
          └── search_customer
                 └── customer_id=123

Model chỉ yêu cầu gọi tool.

Việc thực sự:

search_customer(123)

là bước khác, thường do agent/tool execution layer thực hiện.

6. Đây chính là lý do code LangGraph của bạn có active_tools

Trong project của bạn:

tools = state.get("active_tools") or []

sau đó có thể:

llm_with_tools = llm.bind_tools(tools)

Luồng thực tế là:

User question
     │
     ▼
Tool RAG
     │
     │ tìm tools phù hợp
     ▼
active_tools
     │
     ▼
llm.bind_tools(active_tools)
     │
     ▼
LLM
     │
     ├── không cần tool
     │       ↓
     │      answer
     │
     └── cần tool
             ↓
          tool_calls
             ↓
          Evaluator
             ↓
          Execute

Cho nên bind_tools() là cầu nối giữa LLM và danh sách tools mà Tool-RAG của bạn vừa tìm được.

7. Một cách phân biệt rất chuẩn

Bạn nên ghi chú kiến trúc như này:

00 — langchain_core
     │
     ├── Runnable
     ├── BaseChatModel
     ├── BaseTool
     ├── AIMessage
     └── các abstraction/interface
              │
              ▼
01 — Integration packages
     │
     ├── langchain_ollama
     │      └── ChatOllama
     │
     ├── langchain_openai
     │      └── ChatOpenAI
     │
     └── langchain_google_genai
            └── ChatGoogleGenerativeAI
              │
              ▼
02 — Provider
     │
     ├── Ollama
     ├── OpenAI
     └── Gemini

Và:

llm.bind_tools(tools)

nên được hiểu là:

Application gọi API theo abstraction của LangChain Core → implementation cụ thể (ChatOllama, ChatOpenAI, ...) xử lý nó → chuyển thành request phù hợp cho provider.

Đây cũng là lý do bạn thấy cùng một kiểu code:

llm.invoke(...)
llm.ainvoke(...)
llm.bind_tools(...)

hoạt động với nhiều model khác nhau. API thống nhất nằm ở abstraction của LangChain Core; integration package chịu trách nhiệm hiện thực abstraction đó cho từng provider.



llm_with_tools
    ↓
Runnable

API hiện tại ghi return type là:

Runnable[LanguageModelInput, AIMessage]

Nói đơn giản:

llm

là model bình thường.

Còn:

llm_with_tools

là model đã được cấu hình để tool calling.

5. Khi nào mới thực sự gọi model?

Phải:

response = llm_with_tools.invoke(
    "Tôi muốn xem thông tin tài khoản của tôi"
)

Lúc này mới có:

User
 │
 │ "Tôi muốn xem thông tin tài khoản"
 ↓
llm_with_tools
 │
 │ model suy luận
 ↓
AIMessage

Nếu model quyết định gọi tool:

response.tool_calls

có thể nhận:

[
    {
        "name": "get_user_info",
        "args": {},
        "id": "call_xxx",
        "type": "tool_call"
    }
]

Đây là behavior được mô tả trong docs của ChatOllama.

6. Đây là chỗ nhiều người nhầm nhất

Bạn có:

llm_with_tools = llm.bind_tools(tools)

Không có nghĩa:

bind_tools
   ↓
chạy tool

Mà là:

bind_tools
   ↓
đăng ký / mô tả tools cho model
   ↓
model biết những tool nào nó có thể yêu cầu

Sau đó:

invoke()
   ↓
LLM quyết định
   ↓
có cần tool không?

Nếu có:

AIMessage
   ↓
tool_calls
   ↓
ToolExecutor / ToolNode
   ↓
thực thi Python function
7. tool_choice là gì?

Signature:

llm.bind_tools(
    tools,
    tool_choice=None
)

Theo API hiện tại, tool_choice có thể nhận các dạng như:

None
"auto"
"any"
True / False
dict

nhưng đối với ChatOllama, tool_choice hiện được docs ghi là bị bỏ qua vì Ollama không hỗ trợ parameter này theo cách đó.

Ví dụ với một số integration khác người ta có thể làm:

llm.bind_tools(
    tools,
    tool_choice="any"
)

ý tưởng là:

"Model phải sử dụng tool."

Nhưng với ChatOllama hiện tại, đừng dựa vào tool_choice để ép Ollama gọi một tool cụ thể, vì parameter này được ghi rõ là ignored.

8. **kwargs là gì?

Phần:

**kwargs

cho phép truyền thêm tham số xuống self.bind(...).

Ví dụ về mặt cơ chế:

llm.bind_tools(
    tools,
    some_parameter=...
)

thì các keyword argument bổ sung sẽ được chuyển tiếp.

Nhưng khi dùng ChatOllama, bạn thường không cần quan tâm **kwargs ở bước đầu học tool calling.

9. Liên hệ với @tool bạn hỏi lúc trước

Bạn có:

@tool(
    "get_user_info",
    args_schema=GetUserInfoInput
)
def get_user_info() -> str:
    """
    Lấy thông tin người dùng.
    """
    ...

Sau đó:

llm_with_tools = llm.bind_tools([
    get_user_info
])

Có thể hình dung toàn bộ quá trình:

                  @tool
                    │
                    ▼
          ┌───────────────────┐
          │ get_user_info     │
          │                   │
          │ name              │
          │ description       │
          │ args_schema       │
          │ function          │
          └─────────┬─────────┘
                    │
                    │ bind_tools()
                    ▼
          ┌───────────────────┐
          │    ChatOllama     │
          │ + tool schema     │
          └─────────┬─────────┘
                    │
                    │ invoke()
                    ▼
                 LLM
                    │
             ┌──────┴──────┐
             │             │
          trả lời        gọi tool
          trực tiếp         │
                            ▼
                       tool_calls
10. Còn ToolExecutor nằm ở đâu?

Đây mới là kiến trúc đầy đủ:

User
 │
 │ "Cho tôi xem thông tin tài khoản"
 ↓
ChatOllama
 + bind_tools([get_user_info])
 │
 │ model quyết định
 ↓
AIMessage
 │
 └── tool_calls
       │
       │ name = get_user_info
       │ args = {}
       ↓
ToolExecutor / ToolNode
       │
       ↓
get_user_info(...)
       │
       ↓
Repository
       │
       ↓
MySQL
       │
       ↓
ToolMessage
       │
       ↓
ChatOllama
       │
       ↓
Final answer

Đây chính là lý do đoạn code trước của bạn có:

raise NotImplementedError("Executed via ToolExecutor")

Nếu project của bạn thiết kế theo architecture này thì get_user_info được khai báo cho LLM, còn Executor mới là thằng thực thi logic thật.

11. Một ví dụ hoàn chỉnh tối giản
from langchain_core.tools import tool
from langchain_ollama import ChatOllama


@tool
def add(a: int, b: int) -> int:
    """Add two integers."""
    return a + b


llm = ChatOllama(
    model="qwen3.5:4b",
    temperature=0,
)

llm_with_tools = llm.bind_tools([add])

response = llm_with_tools.invoke(
    "What is 10 + 20?"
)

print(response)
print(response.tool_calls)

Model có thể trả:

response.tool_calls
[
    {
        "name": "add",
        "args": {
            "a": 10,
            "b": 20
        },
        "id": "call_xxx",
        "type": "tool_call"
    }
]

Chú ý: ở thời điểm này add(10, 20) có thể chưa được Python thực thi. AIMessage.tool_calls chỉ là model nói:

"Tôi muốn gọi tool add với a=10, b=20."

Sau đó executor mới lấy name + args để thực thi tool.

Đây là điểm cốt lõi của tool calling: bind_tools() đưa khả năng/tool schema vào model; invoke() nhận quyết định tool-call từ model; executor mới thực sự chạy function.