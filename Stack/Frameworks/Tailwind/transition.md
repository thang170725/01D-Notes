Chuẩn rồi, bạn chỉ thiếu transition thôi 👍
hover: chỉ đổi trạng thái, còn độ chậm (0.5s) phải do transition điều khiển.

✅ Cách làm ĐÚNG trong Tailwind (0.5s)
<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors duration-500">
  <a href="">Dashboard</a>
</li>

Giải thích nhanh

transition-colors → chỉ animate màu (nhẹ & mượt)

duration-500 → 500ms = 0.5s

Hover vào / ra đều mượt

🎯 Muốn mượt hơn (ease)
<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors duration-500 ease-in-out">

🔥 Nếu muốn delay 0.5s (đợi rồi mới đổi)

Khác với duration nhé

<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors delay-500">

❌ Lỗi hay gặp
hover:duration-500   // ❌ sai

duration-0.5s       // ❌ Tailwind không dùng giây

🧠 Nhớ nhanh
Hiệu ứng	Class
Chuyển màu chậm 0.5s	transition-colors duration-500
Đợi 0.5s mới đổi	delay-500
Mượt	ease-in-out
✅ Ví dụ hoàn chỉnh cho sidebar menu
<li className="p-2 rounded-md cursor-pointer
               hover:bg-[oklch(50%_0.066_243.157)]
               transition-colors duration-500 ease-in-out">
  Dashboard
</li>


Nếu bạn muốn hover có slide / fade / scale cho menu sidebar, nói mình biết style bạn muốn, mình làm luôn cho 😄
<li className='p-2 hover:bg-[oklch(50%_0.066_243.157)]'><a href="">Dashboard</a></li>