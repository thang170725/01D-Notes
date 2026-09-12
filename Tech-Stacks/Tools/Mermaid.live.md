- [Mermaid Live Introduction (vẽ sơ đồ bằng code, rất phổ biến trong lập trình và tài liệu kỹ thuật)](#mermaid-live-introduction-vẽ-sơ-đồ-bằng-code-rất-phổ-biến-trong-lập-trình-và-tài-liệu-kỹ-thuật)
- [flowchart ... (Chỉ đinh muốn vẽ sơ đồ luồng)](#flowchart--chỉ-đinh-muốn-vẽ-sơ-đồ-luồng)
- [Tạo node](#tạo-node)
- [Vẽ mũi tên](#vẽ-mũi-tên)
- [Vẽ hình chữ nhật bo góc](#vẽ-hình-chữ-nhật-bo-góc)
- [Vẽ hình oval](#vẽ-hình-oval)
- [Vẽ hình chữ nhâtj góc vuông](#vẽ-hình-chữ-nhâtj-góc-vuông)
- [Vẽ hình thoi](#vẽ-hình-thoi)
- [Vẽ hình tròn](#vẽ-hình-tròn)
- [subgraph (gom nhóm các bước xử lý lâij thành từng khung riêng biệt có tiêu đề)](#subgraph-gom-nhóm-các-bước-xử-lý-lâij-thành-từng-khung-riêng-biệt-có-tiêu-đề)
- [Practices](#practices)
---
# Mermaid Live Introduction (vẽ sơ đồ bằng code, rất phổ biến trong lập trình và tài liệu kỹ thuật)
```bash
Hiểu đơn giản: Thay vì bạn dùng chuột kéo từng ô như Draw.io, 
    bạn viết -> Mermaid sẽ tự biến đoạn code đó thành sơ đồ: User → API → Database → API → User

Nó hỗ trợ rất nhiều loại sơ đồ như:
    - Flowchart
    - Sequence Diagram
    - ER Diagram
    - Class Diagram
    - State Diagram
    - Mindmap
    - Architecture Diagram
    - Gantt
    - Git Graph
    - C4 Diagram
    - Timeline
    - Kanban
    - v.v.
```
# flowchart ... (Chỉ đinh muốn vẽ sơ đồ luồng)
**Syn**
```bash
flowchart TD

- flowchart = loại sơ đồ
- TD       = Top → Down, vẽ từ trên xuống
    + TD:	Top → Down
    + TB:	Top → Bottom
    + LR:	Left → Right
    + RL:	Right → Left
```
**Ex**
```bash
flowchart LR
    A --> B
    B --> C
```
# Tạo node
**Ex**
```bash
flowchart TD
    A
    B
    C
```
# Vẽ mũi tên
**Ex**
```bash
flowchart TD
    A --> B
```
**Ex2: mũi tên có chữ**
```bash
flowchart TD
    A -->|CALL_TOOL| B
```
# Vẽ hình chữ nhật bo góc
```bash
NODE["Nội dung"]
```
# Vẽ hình oval
```bash
START([USER])
```
# Vẽ hình chữ nhâtj góc vuông
```bash
REWRITE["Rewrite User Query"]
```
# Vẽ hình thoi 
```bash
DECISION{"Có hợp lệ không?"}
```
# Vẽ hình tròn
```bash
NODE((Text))
```
# subgraph (gom nhóm các bước xử lý lâij thành từng khung riêng biệt có tiêu đề)
```bash
subgraph PREP["① QUERY PREPARATION"]
    REWRITE["rewrite<br/>Rewrite User Query"]
end
```
subgraph ID["Tên hiển thị"]: Bắt đầu một nhóm.

Chèn các Node thuộc nhóm đó vào giữa.

end: Kết thúc nhóm.

4. Tạo Liên kết (Arrows / Edges) & Nhãn trên đường nối
Các kiểu đường nối:
A --> B: Mũi tên nhọn (Thường dùng nhất).

A --- B: Đường thẳng không mũi tên.

A -.- B: Đường nét đứt.

A -.-> B: Đường nét đứt có mũi tên.

A ==> B: Đường mũi tên nét đậm.

Thêm nhãn (Text) lên đường nối:
Có 2 cách viết phổ biến:

Cách 1 (Dùng thanh đứng |text| - Giống trong code của bạn):

Đoạn mã
AGENT -->|CALL_TOOL| EXECUTE
Cách 2 (Viết trực tiếp -- text -->):

Đoạn mã
AGENT -- CALL_TOOL --> EXECUTE
5. Tùy chỉnh Màu sắc & Giao diện (Styling with Classes)
Để sơ đồ nhìn chuyên nghiệp hơn, Mermaid cho phép bạn định nghĩa các bộ màu (Class) và gán cho từng Node.

Bước 1: Định nghĩa bộ màu (classDef)
Cú pháp: classDef tên_class property:value,property:value...

Đoạn mã
classDef startEnd fill:#1f2937,color:#fff,stroke:#111827,stroke-width:2px
fill:#1f2937: Màu nền của Node.

color:#fff: Màu chữ.

stroke:#111827: Màu viền.

stroke-width:2px: Độ dày viền.

Bước 2: Gán bộ màu cho các Node (class)
Cú pháp: class danh_sách_node tên_class

Đoạn mã
class START,END startEnd
class EXECUTE,RESULT_EVAL tool
(Gán class startEnd cho cả 2 node START và END cùng một lúc).

🛠️ Bài tập thực hành nhỏ cho bạn
Dựa trên các cú pháp trên, bạn hãy thử tự gõ lại một đoạn Mermaid ngắn về Luồng làm sạch OCR đơn giản:

Có START (Oval) → đọc file JSON.

Đưa vào subgraph tên là "Processing".

Rẽ nhánh: Nếu file lỗi → Báo lỗi; Nếu đúng → Save vào DB.

END (Oval).

Bạn có muốn gõ thử đoạn mã đó ra đây để tôi kiểm tra cú pháp giúp bạn không?
# Practices
flowchart TD
    START([USER])

    REWRITE["NODE 1: Rewrite User Query"]

    RETRIEVE["NODE 2: Embed Query<br/>↓<br/>Cosine Similarity<br/>↓<br/>Top-K Tools"]

    AGENT{"NODE 3:<br> AGENT"}

    EXECUTE["NODE 4.1:<br>Execute Tool Calls"]

    DECISION_VALIDATOR{"NODE 4.2:<br>VALIDATOR NO TOOL"}

    RESULT_EVAL{"NODE 5:<br>Evaluate Tool Result"}

    END([END])

    START --> REWRITE
    REWRITE --> RETRIEVE
    RETRIEVE --> AGENT

    AGENT -->|CALL_TOOL| EXECUTE
    AGENT -->|NO_TOOL| DECISION_VALIDATOR
    AGENT -->|REWRITE| REWRITE
    AGENT -->|FINAL| END

    DECISION_VALIDATOR --> |YES| END
    DECISION_VALIDATOR --> |NO| REWRITE

    EXECUTE --> RESULT_EVAL


    RESULT_EVAL -->|YES| AGENT
    RESULT_EVAL -->|NO| REWRITE

    classDef startEnd fill:#1f2937,color:#fff,stroke:#111827,stroke-width:2px
    classDef process fill:#dbeafe,color:#1e3a8a,stroke:#3b82f6,stroke-width:2px
    classDef rag fill:#dcfce7,color:#14532d,stroke:#22c55e,stroke-width:2px
    classDef decision fill:#fef3c7,color:#78350f,stroke:#f59e0b,stroke-width:2px
    classDef tool fill:#f3e8ff,color:#581c87,stroke:#a855f7,stroke-width:2px

    class START,END startEnd
    class REWRITE,AGENT process
    class RETRIEVE rag
    class EXECUTE,RESULT_EVAL tool
    class DECISION decision