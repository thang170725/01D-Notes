- [MCP Introduction (là giao thức để AI nói chuyện với Tool)](#mcp-introduction-là-giao-thức-để-ai-nói-chuyện-với-tool)
---
# MCP Introduction (là giao thức để AI nói chuyện với Tool)
**Ví dụ**
```bash
Giả sử bạn có AI Agent.
    User  
    ↓
    Gemini
    ↓
    MariaDB

Gemini không biết cách kết nối MariaDB. Bạn phải viết:
    - get_user()
    - get_workout()
    - create_plan()
    - delete_plan()
=> rồi truyền cho Gemini. Điều này ổn.

Nhưng nếu sau này. Bạn có thêm
    - Google Calendar
    - Notion
    - Slack
    - GitHub
    - Qdrant
    - Redis
    - Stripe
=> Bạn sẽ phải viết rất nhiều Tool.

Không có MCP
    Gemini
    │
    ├── Tool A
    ├── Tool B
    ├── Tool C
    ├── Tool D
    ├── Tool E
    ├── Tool F

Mỗi Tool
    - Có format khác nhau.
    - Có auth khác nhau.
    - Có schema khác nhau.
    - AI phải học từng cái.

Có MCP
    Gemini 
    ↓
    MCP
    ↓
    Google Calendar
    ↓
    Notion
    ↓
    Slack
    ↓
    MariaDB
    ↓
    GitHub
=> AI chỉ cần biết "Nói chuyện bằng MCP." Không cần quan tâm Tool bên dưới viết bằng Python, NodeJS hay Go.
```
**Ex**
```bash
Bạn có Database. MariaDB

Bạn viết MCP Server Bên trong.
    - get_user()
    - create_workout()
    - delete_workout()
    - get_recipe()
=> Gemini không gọi Python trực tiếp.
    Gemini
    ↓
    MCP
    ↓
    Tool.
```