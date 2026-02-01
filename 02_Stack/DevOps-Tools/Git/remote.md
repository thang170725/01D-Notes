git clone 
Lệnh này giúp bạn sao chép toàn bộ mã nguồn, lịch sử thay đổi, nhánh, commit, và tất cả các file trong dự án về máy tính để làm việc trực tiếp.
Cú pháp:
git clone https://github.com/thang1707/lesson1.git dev1 (Sao chép ma nguồn từ gitHub và thư mục dev1)
git clone --branch khue --single-branch https://github.com/thang170725/elgamal.git (clone nhánh cụ thể về máy tính)
git remote
Dùng để kết nối môt repository git cục bộ (trên máy tính của bạn) với một repository từ xa (trên gitHub). giúp git push và git pull. Khi bạn khởi tạo một repository mới trên máy (git init), nó chưa biết liên kết với nơi nào để push code lên
Dùng khi bạn đã có sẵn code trên máy và muốn đẩy dự án này lên gitHub.
Cú pháp:
    1. git remote -v (Xem remote hiện tại là gì)
    2. git remote add origin https://github.com/thang1707/an_toan_bao_mat_tt.git
    3. git remote set-url origin https://github.com/thang170725/elgamal.git (Khi bạn muốn dùng remote origin nhưng trỏ tới repo mới)
    4. git push
Cú pháp:
    1. git push origin cong (push code vào nhánh cong)
git pull
Lấy dữ liệu và hợp nhất (merge) những thay đổi đó vào nhánh hiện tại của bạn. Lệnh này là sự kết hợp của 2 lệnh git fetch (lấy các thay đổi từ kho lưu trữ từ xa) và git merge (hợp nhất các thay đổi vào nhánh hiện tại)
Cú pháp:
    1. git pull origin main (pull từ nhánh main)
    2. git pull --no-rebase origin main