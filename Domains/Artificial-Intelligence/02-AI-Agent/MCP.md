- [MCP Introduction (là giao thức để AI nói chuyện với Tool)](#mcp-introduction-là-giao-thức-để-ai-nói-chuyện-với-tool)
---
# MCP Introduction (là giao thức để AI nói chuyện với Tool)
**Tại sao cần MCP?**
```bash
Giả sử bạn xây dựng một AI Agent: User → Gemini → MariaDB`

Gemini không thể tự truy cập MariaDB. Bạn phải cung cấp cho Gemini các Tool để thực hiện nghiệp vụ:
    - `get_user()`
    - `get_workout()`
    - `create_plan()`
    - `delete_plan()`

Bạn tự viết các hàm Python, sau đó đăng ký chúng với Gemini thông qua Function Calling.
    Điều này hoàn toàn ổn nếu hệ thống chỉ có một AI Agent và một số Tool nội bộ.

Nhưng vấn đề xuất hiện khi hệ thống phát triển:
    Bạn muốn Agent có thể sử dụng thêm:
        + Google Calendar
        + Notion
        + Slack
        + GitHub
        + Qdrant
        + Redis
        + Stripe

    Lúc này có hai vấn đề:
        - Vấn đề 1: Khả năng tái sử dụng
            + Giả sử sau này bạn muốn chuyển từ Gemini sang GPT hoặc Claude.
            + Nếu không sử dụng MCP, bạn có thể phải viết lại phần tích hợp Tool theo định dạng Function Calling của từng nền tảng AI.
            + Mặc dù vẫn có thể tái sử dụng logic nghiệp vụ, bạn vẫn phải tự xây dựng các adapter để chuyển đổi schema, request và response.
        - Vấn đề 2: Không phải lúc nào bạn cũng cần tự viết Tool
            + Ví dụ GitHub đã có MCP Server cung cấp các chức năng như:
                - Tìm kiếm repository.
                - Đọc nội dung file.
                - Tạo Pull Request.
                - Quản lý Issue.
            - Thay vì tự viết từng API wrapper cho GitHub, bạn có thể kết nối với GitHub MCP Server và sử dụng những Tool mà nó cung cấp.
```
*Không có MCP*
```bash
Gemini ── Function Calling ── Python Tools ── GitHub API
GPT    ── Function Calling ── Python Tools ── GitHub API
Claude ── Function Calling ── Python Tools ── GitHub API

Mỗi nền tảng AI có thể cần một lớp tích hợp riêng.
    Bạn phải tự xử lý:
        - Schema Tool theo từng nền tảng.
        - Chuyển đổi request/response.
        - Authentication.
        - Tích hợp và bảo trì.
```
*Có MCP*
```bash
Gemini ──┐
GPT    ──┼── MCP Client
Claude ──┘       │
                 ├── GitHub MCP Server ── GitHub API
                 ├── Notion MCP Server  ── Notion API
                 └── Slack MCP Server   ── Slack API

Các AI Client có thể giao tiếp với MCP Server thông qua cùng một giao thức MCP.
Mỗi MCP Server có thể được viết bằng Python, TypeScript, Go hoặc ngôn ngữ khác. Client không cần quan tâm Server được triển khai bằng ngôn ngữ nào.
```
**Vậy MCP mang lại lợi ích gì?**
```bash
1. **Chuẩn hóa giao tiếp:** Không cần xây dựng một giao thức tích hợp Tool riêng cho từng nền tảng AI.
2. **Tái sử dụng:** Một MCP Server có thể phục vụ nhiều MCP Client.
3. **Tận dụng hệ sinh thái:** Có thể sử dụng MCP Server do nhà cung cấp hoặc cộng đồng xây dựng, không cần tự viết lại tất cả API wrapper.
4. **Tách biệt hệ thống:** AI Client không cần biết chi tiết cách MCP Server triển khai và giao tiếp với hệ thống bên dưới.
```