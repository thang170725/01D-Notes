- [StateGraph](#stategraph)
- [END](#end)
  - [.add\_node()](#add_node)
  - [.set\_entry\_point()](#set_entry_point)
  - [.add\_edge()](#add_edge)
  - [.add\_conditional\_edges()](#add_conditional_edges)
  - [.compile()](#compile)
  - [.invoke()](#invoke)
  - [.stream()](#stream)
---
# StateGraph
```bash
Tạo graph với state kiểu TypedDict.
```
**Syn**
```bash
from langgraph.graph import StateGraph, END

graph = StateGraph(StateType)
```
# END
```bash
Dùng để kết thúc graph
```
**Syn**
```bash
graph.add_edge("node_name", END)
```
## .add_node()
```bash
Thêm một bước xử lý
```
**Syn**
```bash
graph.add_node("node_name", function)

- "node_name" = tên node
- function = hàm xử lý state
```
## .set_entry_point()
```bash
Định nghĩa node bắt đầu
```
## .add_edge()
```bash
Nối node A → B hoặc kết thúc
```
**Syn**
```bash
- graph.add_edge("node_a", "node_b")
- graph.add_edge("node_a", END)
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
