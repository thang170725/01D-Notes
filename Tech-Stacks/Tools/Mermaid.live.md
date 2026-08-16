À 😄 Mermaid Live (mermaid.live) thì khác hoàn toàn.

Nó là trình vẽ sơ đồ bằng code, rất phổ biến trong lập trình và tài liệu kỹ thuật.

Mermaid Live Editor

Hiểu đơn giản

Thay vì bạn dùng chuột kéo từng ô như Draw.io, bạn viết:

Mermaid sẽ tự biến đoạn code đó thành sơ đồ:

User → API → Database → API → User

Nó hỗ trợ rất nhiều loại sơ đồ như:

Flowchart
Sequence Diagram
ER Diagram
Class Diagram
State Diagram
Mindmap
Architecture Diagram
Gantt
Git Graph
C4 Diagram
Timeline
Kanban
v.v.
Với việc bạn đang code thì nó khá hữu ích

Đặc biệt nếu bạn đang làm project Python/pipeline như json_service, bạn có thể dùng Mermaid để vẽ:

Input JSON
    ↓
Loader
    ↓
Builder
    ↓
Table Builder
    ↓
Saver
    ↓
Output

và AI như ChatGPT/Claude cũng có thể viết Mermaid code cho bạn. Sau đó chỉ cần paste vào Mermaid Live để xem sơ đồ.

Một điểm hay nữa là Mermaid là diagram-as-code: sơ đồ nằm dưới dạng text/code nên rất dễ đưa vào Git, README và tài liệu dự án. Mermaid Live Editor cũng cho phép preview realtime và export SVG/PNG/Markdown.

Nếu bạn đang dùng Aider + Git, mình đánh giá Mermaid khá đáng học vì nó hợp với workflow code-first hơn Draw.io. Bạn có thể bảo Aider:

"Vẽ architecture của project này bằng Mermaid"

rồi lấy code Mermaid đó đưa thẳng vào README.

Tiếp tục khám phá:

Vẽ architecture project bằng Mermaid
Tạo sequence diagram cho luồng xử lý JSON