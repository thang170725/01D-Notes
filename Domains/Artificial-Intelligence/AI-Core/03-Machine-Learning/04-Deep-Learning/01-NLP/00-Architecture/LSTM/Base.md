- [Introduction](#introduction)
---
# Introduction
```bash
LSTM (Long Short-Term Memory) giải quyết việc mất trí nhớ của RNN.

LSTM tách biệt hoàn toàn hai khái niệm: 
    - Hidden State (trạng thái ẩn) 
    - Cell State (trạng thái ô - đóng vai trò như một đường băng chuyền thông tin xuyên suốt). 
    - Thêm cấu trúc “cổng” (gate) và có cell state giúp duy trì thông tin dài hạn.

Cơ chế 3 Cổng (Gates): Hãy tưởng tượng Cell State là một băng tải chạy dọc từ đầu đến cuối chuỗi.\n Các cổng sẽ quyết định cái gì được đặt lên hoặc nhấc ra khỏi băng tải đó:
    - Forget Gate (Cổng quên): "Chúng ta nên bỏ bớt cái gì cũ không?"
        + Nó nhận đầu vào xt​ và ht−1​, đi qua hàm Sigmoid (cho ra giá trị từ 0 đến 1).
        + Nếu là 0: Xóa bỏ hoàn toàn thông tin cũ. Nếu là 1: Giữ lại toàn bộ.
    - Input Gate (Cổng vào): "Có thông tin mới nào đáng giá để lưu lại không?"
        + Gồm 2 phần: 
            - Một hàm Sigmoid quyết định cập nhật cái gì 
            - một hàm tanh tạo ra một vector giá trị mới tiềm năng để đưa vào Cell State.
    - Output Gate (Cổng ra): "Từ những gì đang có, chúng ta nên xuất bản cái gì ra ngoài?"
        + Nó quyết định giá trị nào trong Cell State sẽ được dùng để tạo ra Hidden State (ht​) cho bước tiếp theo. 

Ưu điểm: Nhớ được thông tin xa hơn, Giảm vanishing gradient, Ổn định hơn khi xử lý văn bản dài
```