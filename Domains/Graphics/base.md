7. Đồ họa
Particle System (Hệ thống hạt)
Implicit Geometry (Toán học ẩn)
Công thức mô phỏng sử đàn hồi
    • Trong tự nhiên, hầu hết các quá trình "thả lỏng" hay "hồi phục" đều không diễn ra đều đặn theo đường thẳng.
    • Ví dụ thực tế: Khi bạn kéo một sợi dây thun rồi thả tay ra, hoặc khi nhún một chiếc lò xo, lực kéo về lúc đầu rất mạnh (tốc độ phục hồi cực nhanh), sau đó chậm dần lại khi nó gần về vị trí cũ.
    • Toán học hóa: Hàm y=e**−x mô tả chính xác điều này. Nó giảm rất nhanh ở giai đoạn đầu và "tiệm cận" (về gần 0) một cách êm ái ở giai đoạn sau.
Ví dụ:
Công thức gốc: 1.3 * np.exp(-4.0 * x)

    • Dấu trừ (-): Để hàm giảm đi (xẹp lại). Nếu là dấu cộng, trái tim sẽ nổ tung vì phình ra vô tận.
    • Con số 4.0: Đây là hệ số tốc độ (Decay rate).
        ◦ Nếu số này lớn (ví dụ 10.0): Trái tim xẹp lại cực nhanh, tạo cảm giác giật cục.
        ◦ Nếu số này nhỏ (ví dụ 1.0): Trái tim xẹp lại rất chậm, lờ đờ.
        ◦ Tác giả chọn 4.0 vì nó tạo ra độ trễ vừa phải, đủ để mắt người cảm nhận được độ "mềm" của cơ tim.

Point Cloud (hình ảnh đám mây điểm)
First-order approximation
Dùng để tính xấp xỉ khoảng cách

Hình trái tim
Phương trình:
Phương trình mặc ẩn: F(x, y, z) = ( (x**2 + (49/9)*y**2 + z**2 – 1)**3 - x**2 * z**3 - (80/9) * y**2 * z**3)

