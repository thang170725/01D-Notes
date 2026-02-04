GIL (Global Interpreter Lock)
    • GIL (Global Interpreter Lock) là một cơ chế khóa trong CPython (trình thông dịch Python phổ biến nhất). Tại mọi thời điểm, chỉ có 1 thread được phép thực thi Python bytecode, dù máy có nhiều CPU core.
    • Ví dụ:
        ◦ Thread: 1 người cầm chìa khóa (GIL), nhiều người xếp hàng
        ◦ Process: mỗi người có chìa khóa riêng chạy độc lập
