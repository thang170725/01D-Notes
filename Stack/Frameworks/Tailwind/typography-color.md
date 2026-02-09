```bash
- Dùng để xử lý màu sắc (text-color, background-color, border-color).
```
- [text (Màu chữ)](#text-màu-chữ)
---
# text (Màu chữ)
**Ex1**
```js
<p className="text-red-500">Red text</p>
<p className="text-blue-600">Blue text</p>
<p className="text-slate-800">Dark text</p>
<p className="text-[#ff5733]">Custom color</p>
<p className="text-[rgb(255,255,255)]">White</p>
<p className="text-[rgba(255,255,255,0.7)]">White 70%</p>
<p className="text-[oklch(95%_0.01_240)]">Text OKLCH</p>
```
# background
<div className="bg-red-500"></div>
<div className="bg-blue-100"></div>
<div className="bg-slate-800"></div>

Màu HEX / RGB / custom (chuẩn giống w-[200px])
<div className="bg-[#ff5733]"></div>
<div className="bg-[rgb(255,0,0)]"></div>
<div className="bg-[rgba(0,0,0,0.5)]"></div>


🔥 Rất hay dùng khi design có màu riêng

🖼 Background image
Dùng URL trực tiếp
<div className="bg-[url('/images/bg.png')] bg-cover bg-center"></div>


Các class hay đi kèm:

bg-cover     // cover full
bg-contain   // vừa ảnh
bg-center    // căn giữa
bg-no-repeat // không lặp

🌈 Background gradient
<div className="bg-gradient-to-r from-blue-500 to-purple-500"></div>


Hoặc custom màu:

<div className="bg-gradient-to-r from-[#ff5733] to-[#00ffcc]"></div>
✅ Border cơ bản
<div className="border">...</div>


👉 mặc định: 1px solid #e5e7eb

🎨 Border màu
border-red-500
border-slate-300
border-[#ff5733]