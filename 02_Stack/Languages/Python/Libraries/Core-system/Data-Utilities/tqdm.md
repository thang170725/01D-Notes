Tqdm
Để tạo thanh tiến trình, thường dùng khi có vòng lặp chạy lâu.
pip install tqdm
Cú pháp:
from tqdm import tqdm
import time

for i in tqdm(range(10)):
    time.sleep(0.5) 
# có thanh tiến trình xuất hiện và tăng lên sau mỗi 0.5s
