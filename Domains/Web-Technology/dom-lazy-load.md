```bash
- Web hiện đại KHÔNG load 1 lần
- Có 3 tầng:
    + HTML khung (load ngay)
    + JS render DOM
    + JS fetch data khi có event (scroll, focus, viewport xuất hiện)


🧪 BÀI TEST 1 (BẮT BUỘC)

👉 Không viết crawler, chỉ debug:

Mở devtools

Reload page detail

KHÔNG scroll

Gõ trong console:

document.querySelectorAll('.re__pr-specs-content-item').length


👉 Sau đó scroll xuống → gõ lại

❓ Câu hỏi bạn phải trả lời được:

Trước scroll là bao nhiêu?

Sau scroll là bao nhiêu?

Vậy lỗi nằm ở Python hay JS?

📌 Khi bạn trả lời được → sang phần 2