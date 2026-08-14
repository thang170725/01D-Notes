- [Aider Introduction (là một AI coding assistant chạy trong terminal, giúp bạn viết và sửa code bằng cách chat với AI)](#aider-introduction-là-một-ai-coding-assistant-chạy-trong-terminal-giúp-bạn-viết-và-sửa-code-bằng-cách-chat-với-ai)
- [Installation](#installation)
- [Cấu hình API key](#cấu-hình-api-key)
- [run](#run)
- [Ask](#ask)
  - [So sánh Aider và Cursor](#so-sánh-aider-và-cursor)
  - [Nên chọn Cursor hay Aider?](#nên-chọn-cursor-hay-aider)
  - [nên cài Aider vào môi trường ảo hay global](#nên-cài-aider-vào-môi-trường-ảo-hay-global)
---
# Aider Introduction (là một AI coding assistant chạy trong terminal, giúp bạn viết và sửa code bằng cách chat với AI)
```bash
Hiểu đơn giản:
    1. Bạn mở terminal → chạy aider
    2. Chọn model AI (Gemini, Claude, GPT...)
    3. Nói: “Sửa lỗi file check.py này”
    4. Aider đọc code → đề xuất/thực hiện thay đổi trực tiếp vào file.
    5. Nó có tích hợp Git, nên dễ xem và quản lý các thay đổi.
👉 Có thể hiểu Aider ≈ Cursor nhưng hoạt động chủ yếu trong terminal, tập trung vào việc AI chỉnh sửa code trong repo của bạn.
```
# Installation
**Windows**
```bash
Cách 1: Cài trực tiếp vào Môi trường ảo (venv) của dự án (Đề xuất nếu bạn đang bật venv)
    1. .\venv\Scripts\Activate.ps1
    2. pip install aider-chat

    Ưu điểm: Rất nhanh, gọn, Aider nằm gọn trong môi trường ảo đó và sử dụng đúng phiên bản Python của dự án.

Cách 2: Cài bằng pipx (Cách TỐI ƯU NHẤT để dùng Aider ở MỌI DỰ ÁN)
    Nếu bạn muốn cài Aider 1 lần duy nhất trên máy và từ đó trở đi có thể mở Terminal ở bất kỳ thư mục/dự án nào (dù dự án đó dùng venv hay không) để gọi lệnh aider:

    pipx là công cụ chính chủ của Python chuyên dùng để cài các ứng dụng CLI vào một môi trường ảo riêng ngầm định.
        Cài pipx (nếu chưa có):
            1. pip install pipx
            2. pipx ensurepath
            3. pipx install aider-chat
    
    Ưu điểm vượt trội: Aider sẽ sống trong một môi trường cách ly hoàn toàn, không bao giờ làm hỏng hay đụng chạm đến thư viện của bất kỳ dự án Python nào của bạn, nhưng bạn vẫn có thể gõ lệnh aider ở bất cứ đâu!
```
# Cấu hình API key
**Ex: Cấu hình API key model gemini**
```bash
$env:GEMINI_API_KEY="chuỗi_api_key_vừa_copy"
```
# run
```bash
aider --model gemini/gemini-1.5-flash
```
# Ask 
## So sánh Aider và Cursor
```bash
Nếu nói dễ hiểu nhất:
    - Cursor = IDE có AI bên trong
    - Aider = AI coding agent chạy trong terminal

|                             | **Cursor**                      | **Aider**                              |
| --------------------------- | ------------------------------- | -------------------------------------- |
| Cách dùng                   | Giao diện giống VS Code         | Terminal                               |
| Sửa code                    | Chat + chọn file/code trực tiếp | Chat bằng lệnh, AI tự đọc/sửa file     |
| Xem code                    | Rất tiện, có editor             | Phải mở bằng editor khác hoặc terminal |
| AI làm việc với cả project  | Có                              | Có, khá mạnh                           |
| Git                         | Có giao diện hỗ trợ             | Tích hợp Git rất tự nhiên              |
| Dễ bắt đầu                  | ⭐⭐⭐⭐⭐                   | ⭐⭐⭐                                |
| Phù hợp terminal/CLI        | ⭐⭐⭐                        | ⭐⭐⭐⭐⭐                           |
| Kiểm soát thay đổi bằng Git | ⭐⭐⭐⭐                      | ⭐⭐⭐⭐⭐                           |

Ví dụ:
    Cursor:
        Bạn mở project → mở check.py → chat: "Sửa lỗi hàm này và giải thích cho tôi."

        AI sửa code ngay trong editor, bạn nhìn diff và accept/reject.

    Aider:
        Trong terminal: aider app/utils/check.py
        
        Sau đó:
            > sửa lỗi trong check.py và thêm xử lý exception

        Aider đọc file → sửa file → hiển thị thay đổi → Git giúp bạn quản lý những thay đổi đó.
```
## Nên chọn Cursor hay Aider?
```bash
Chọn Cursor nếu:
    - Bạn thích giao diện IDE.
    - Thường xuyên vừa code + đọc code + debug.
    - Muốn AI autocomplete, chat, chỉnh sửa code ngay trong editor.
    - Muốn trải nghiệm giống VS Code nhưng có AI mạnh hơn.

Chọn Aider nếu:
    - Bạn thích làm việc bằng terminal.
    - Đã quen Git.
    - Muốn AI thao tác trực tiếp trên repo và nhiều file.
    - Muốn dùng nhiều model khác nhau qua API/CLI.
    - Làm việc kiểu: ra task → AI sửa repo → xem diff → commit.
```
## nên cài Aider vào môi trường ảo hay global
```bash
NÊN cài Aider vào Môi trường ảo (Virtual Environment - venv / conda) của dự án, hoặc dùng pipx để cài độc lập ở ngoài.

1. Tại sao KHÔNG nên pip install trực tiếp ở môi trường toàn cục (Global)?
    Nếu bạn dùng lệnh pip install aider-chat ở ngoài môi trường ảo (Global Python):
        - Aider cần cài đặt rất nhiều thư viện phụ thuộc (dependencies) về xử lý Git, LLM, Tokenizer...
        - Việc này dễ làm "rác" môi trường Python toàn cục của máy và dễ gây ra xung đột phiên bản (version conflict) với các thư viện khác mà bạn dùng cho dự án Python cá nhân sau này.
```