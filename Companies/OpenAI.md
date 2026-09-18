+ [<<Back](Base.md)
- [Open AI Introduction (là một công ty nghiên cứu và phát triển AI, nổi tiếng nhất với dòng mô hình GPT và sản phẩm ChatGPT)](#open-ai-introduction-là-một-công-ty-nghiên-cứu-và-phát-triển-ai-nổi-tiếng-nhất-với-dòng-mô-hình-gpt-và-sản-phẩm-chatgpt)
- [ChatGPT Work](#chatgpt-work)
- [Codex (là coding agent của OpenAI)](#codex-là-coding-agent-của-openai)
- [OpenAI API (API cho phép chương trình của bạn gọi các model của OpenAI thay vì bạn phải tự chạy model trên máy)](#openai-api-api-cho-phép-chương-trình-của-bạn-gọi-các-model-của-openai-thay-vì-bạn-phải-tự-chạy-model-trên-máy)
---
# Open AI Introduction (là một công ty nghiên cứu và phát triển AI, nổi tiếng nhất với dòng mô hình GPT và sản phẩm ChatGPT)
```bash
                         OpenAI
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       ChatGPT          API Platform       Codex
          │                │                │
    Người dùng         Developer        Software Engineer
          │                │                │
   Chat / Work       Build AI app       Build / modify code
                           │
                     AI Models + Tools

Hiện tại OpenAI cung cấp cả sản phẩm cho người dùng cuối, doanh nghiệp, và developer xây ứng dụng AI.
OpenAI
   │
   ├── ChatGPT
   │     └── Bạn trực tiếp sử dụng AI
   │
   ├── OpenAI API
   │     └── Python application của bạn gọi AI
   │
   ├── Codex
   │     └── AI agent dành cho software engineering
   │
   └── Business / Enterprise
         └── AI cho tổ chức

Sản phẩm quan trọng nhất: ChatGPT
   ChatGPT là sản phẩm mà người dùng cuối tương tác trực tiếp.

   Bạn có thể dùng nó cho:
      - hỏi đáp
      - học tập
      - lập trình
      - phân tích dữ liệu
      - phân tích file
      - xử lý hình ảnh
      - nghiên cứu
      - viết tài liệu
      - tạo nội dung
      - làm việc với các công cụ
      - thực hiện những workflow nhiều bước
      - ...

OpenAI hiện cũng đang phát triển ChatGPT theo hướng agent, tức là không chỉ "trả lời câu hỏi" mà có thể thực hiện một chuỗi hành động để hoàn thành công việc. ChatGPT agent có khả năng sử dụng công cụ, duyệt web, chạy code, phân tích và tạo các deliverable như spreadsheet hoặc presentation.
```
**Ex: agentic workflow**
```bash
Bạn: "Phân tích 3 đối thủ của công ty tôi và tạo báo cáo"

Agent: Research web -> Thu thập dữ liệu -> Phân tích -> Tổng hợp -> Tạo report -> Đây là một sự thay đổi khá lớn trong cách sử dụng AI.
```
# ChatGPT Work
```bash
Một hướng mới của ChatGPT là phân biệt:
   - Chat
   - Work
   - Codex

Theo tài liệu hiện tại của OpenAI:
   - Chat → câu hỏi, trao đổi, brainstorming nhanh.
   - Work → công việc dài hơn, nghiên cứu, phân tích và tạo deliverable.
   - Codex → software development.
```
**Ex**
```bash
- Chat -> "Giải thích cho tôi OOP là gì?"
- Work -> "Phân tích thị trường AI Việt Nam và tạo báo cáo 20 trang."
- Codex -> "Đọc repository này, refactor architecture và viết test."
```
# Codex (là coding agent của OpenAI)
```bash
Nó không đơn giản chỉ là: AI autocomplete
   Mà hướng tới: Bạn giao task -> Codex đọc repository -> hiểu architecture -> sửa / tạo file -> chạy command -> chạy test -> kiểm tra kết quả -> đề xuất thay đổi
```
# OpenAI API (API cho phép chương trình của bạn gọi các model của OpenAI thay vì bạn phải tự chạy model trên máy)
```bash
OpenAI cung cấp API cho text generation, xử lý ngôn ngữ, vision và nhiều khả năng khác; quickstart hiện tại hướng developer bắt đầu bằng API key và Responses API.
```