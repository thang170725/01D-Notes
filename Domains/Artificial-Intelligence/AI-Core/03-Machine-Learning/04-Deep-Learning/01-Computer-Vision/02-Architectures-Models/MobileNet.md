# MobileNet (2017 – "CNN cho điện thoại")
```bash
Google nhận thấy:
    CNN rất mạnh.

    Nhưng:
        - điện thoại yếu
        - RAM ít
        - CPU chậm
        - pin hạn chế
    => Cần CNN nhỏ hơn.

Ý tưởng
    Conv bình thường rất tốn phép tính.

    Ví dụ:
        - Input: 100×100×64
        - Output: 100×100×128
    => Conv thông thường sẽ phải tính cực kỳ nhiều phép nhân.

    Google tách Conv thành hai bước.
        Bước 1: Depthwise Convolution => Mỗi channel tự Conv riêng.
            Ví dụ: 
                Channel 1
                ↓

                3×3 Conv
                ↓
                Channel 1

                Channel 2
                ↓
                3×3 Conv
                ↓
                Channel 2
            => Không trộn các channel với nhau.

        Bước 2: Pointwise Convolution
            Dùng kernel: 1×1 để trộn các channel.
                64 channels           
                ↓
                1×1 Conv
                ↓
                128 channels

            Lợi ích:
                - Giảm khoảng           
                - 8–9 lần
                - phép tính.
                - Accuracy gần như vẫn giữ nguyên.

MobileNet dùng ở đâu?
    Rất nhiều.

    Ví dụ:
        - Camera điện thoại
        - Face Unlock
        - OCR
        - Object Detection
        - Drone
        - Robot
        - Raspberry Pi
        - IoT
```