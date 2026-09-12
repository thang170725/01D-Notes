- [Langchain](#langchain)
  - [Create \& Config (Nhóm khởi tạo \& cấu hình)](#create--config-nhóm-khởi-tạo--cấu-hình)
    - [create\_agent()](#create_agent)
- [streaming](#streaming)
- [.bind()](#bind)
- [Agent tạo nhanh](#agent-tạo-nhanh)
---
# Langchain
## Create & Config (Nhóm khởi tạo & cấu hình)
### create_agent()
**Syn**
```bash
agent = create_agent(
    model="anthropic:claude-sonnet-4-6",
    tools=[get_weather],
    system_prompt="You are a helpful assistant",
)
```
**Ex**
```python
# pip install -qU langchain "langchain[anthropic]"
from langchain.agents import create_agent

def get_weather(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

agent = create_agent(
    model="anthropic:claude-sonnet-4-6",
    tools=[get_weather],
    system_prompt="You are a helpful assistant",
)

# Run the agent
agent.invoke(
    {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
)
```
# streaming
```bash
- Quan trong khi làm chatbot realtime
```
**Ex**
```python
for chunk in chain.stream({"topic": "AI"}):
    print(chunk, end="")
```

# .bind()
```python
model = ChatOpenAI().bind(
    temperature=0.2,
    max_tokens=200
)

# chain = prompt | model.bind(temperature=0)
```

# Agent tạo nhanh
```bash
from langchain.agents import create_openai_tools_agent
from langchain.agents import AgentExecutor
```
