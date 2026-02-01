CI – Continuous Integration (Tích hợp liên tục)

👉 Lập trình viên code xong là đẩy lên repo (Git) → hệ thống tự động làm tiếp.

CI thường sẽ:

✅ Build code

✅ Chạy test tự động (unit test, lint…)

✅ Kiểm tra lỗi sớm

🎯 Mục tiêu:

Phát hiện bug càng sớm càng tốt

Tránh cảnh “code chạy máy anh, không chạy máy em”

Ví dụ:

Mỗi lần bạn git push, GitHub Actions/Jenkins tự động chạy test.

2️⃣ CD – Continuous Delivery / Continuous Deployment

Có 2 nghĩa CD, hay bị nhầm:

🔹 Continuous Delivery

Code luôn sẵn sàng để deploy

Deploy lên production có thể cần bấm nút xác nhận

🔹 Continuous Deployment

Code pass hết test → tự động deploy thẳng lên production

Không cần con người can thiệp

🎯 Mục tiêu:

Ra feature nhanh

Giảm lỗi khi deploy thủ công

3️⃣ CI/CD hoạt động như thế nào? (Luồng cơ bản)
Dev push code
   ↓
CI: build + test
   ↓
CD: deploy (staging / production)

4️⃣ Công cụ CI/CD phổ biến

🔧 GitHub Actions

🔧 GitLab CI/CD

🔧 Jenkins

🔧 CircleCI

🔧 Azure DevOps

5️⃣ Vì sao CI/CD quan trọng?

🚀 Deploy nhanh, đều, ít lỗi

🧪 Test tự động → code chất lượng hơn

👥 Team làm việc mượt hơn

😌 Đỡ stress mỗi lần release

6️⃣ Ví dụ thực tế (dễ hình dung)

Bạn làm web:

Push code lên GitHub

GitHub Actions:

Chạy test

Build project

Deploy lên server / cloud
👉 Không cần SSH, không cần gõ lệnh tay

Nếu bạn muốn, mình có thể:

Giải thích CI/CD cho người mới học

Cho ví dụ pipeline GitHub Actions

So sánh CI/CD vs deploy thủ công

Áp dụng CI/CD cho backend / frontend / mobile