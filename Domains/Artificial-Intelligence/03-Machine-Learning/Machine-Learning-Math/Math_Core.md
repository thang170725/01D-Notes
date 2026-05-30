- [Phương sai](#phương-sai)
- [Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu](#độ-lệch-chuẩn-tổng-thể-và-độ-lệch-chuẩn-mẫu)
- [Computer Vision](#computer-vision)
  - [Kernel](#kernel)
  - [Gaussian Blur](#gaussian-blur)
  - [Median Blur](#median-blur)
  - [Sharpen (làm sắc nét)](#sharpen-làm-sắc-nét)
  - [Sobel, Laplacian](#sobel-laplacian)
---
# Phương sai
```bash
Phương sai là một số đo cho biết mức độ phân tán của các giá trị trong tập dữ liệu so với giá trị trung bình của tập dữ liệu đó. Phương sai cho biết các giá trị trong tập dữ liệu “lan rộng” ra sao xung quanh giá trị trung bình.
Phương sai càng lớn thì giá trị trong tập dữ liệu càng phân tán xa so với giá trị trung bình và ngược lại.
```
# Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu 
**Ex: 5 số 12,34,45,70,86**
```bash
1. Tính trung bình cộng: (12 + 34 + 45 + 70 + 86) / 5 = 49.4 
2. 
    Tính phương sai mẫu: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / (5-1) = 854.8 
    Tính phương sai tổng thể: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / 5 = 683.84  
3. 
    Tính độ lệch chuẩn của phương sai mẫu: np.sqrt(854.8)= 29.23696291
    Tính độ lệch chuẩn của phương sai tổng thể: np.sqrt(683.84) = 26.15 
```
# Computer Vision
## Kernel
```bash
- Phần lớn các bộ lọc đều dựa trên khái niệm convolution (tích chập) – tức là áp một ma trận (kernel) lên từng vùng nhỏ của ảnh để tính toán giá trị mới cho pixel trung tâm. 
- Cách áp dụng kernel này có một quy tắc chuẩn:
    + Duyệt từng pixel trong ảnh gốc.
    + Với mỗi pixel, lấy vùng lân cận (theo kích thước kernel), nhân chéo với kernel.
    + Tính tổng và gán giá trị kết quả vào pixel tương ứng trong ảnh mới.
```
## Gaussian Blur
```bash
Dùng kernel theo phân phối Gauss – làm mờ mịn, tự nhiên hơn.
```
## Median Blur
```bash
Lấy giá trị trung vị trong vùng lân cận – khử nhiễu muối tiêu.
```
## Sharpen (làm sắc nét)
```bash
Dùng kernel làm nổi bật cạnh, tăng tương phản cục bộ.
```
## Sobel, Laplacian
```bash
Dùng để phát hiện biên cạnh – áp kernel đạo hàm.
```
Thuật toán ID3 (Iterative Dichotomiser 3)
    • Là thuật toán xây dựng cây quyết định bằng cách chọn thuộc tính “tốt nhất” để chia dữ liệu tại mỗi bước.
    • Thuộc tính “tốt nhất” được chọn dựa trên việc giảm độ hỗn loạn (entropy) nhiều nhất → nghĩa là giúp dữ liệu trở nên “thuần” nhất có thể.
Entropy (độ hỗn loạn):
Cho biết một tập dữ liệu có lẫn lộn hay không. (Khi chia dữ liệu theo thuộc tính A thì độ hỗn loạn mới là bao nhiêu)
Công thức:
Entropy(S) = -[p1.log2(p1) + p2.log2(p2) + … ]
    • pi: phần trăm mẫu thuộc lớp i (ví dụ: [‘no’, ‘no’, ‘yes’, ‘yes’, ‘yes’] thì p_no = 2/5). Nếu tập đã thuần (100% Yes) → entropy = 0 (không hỗn loạn).
    • Nếu chia đều (50% Yes - 50% No) → entropy = 1 (hỗn loạn tối đa).
EntropyA(S) = [(|Sv1| / S) * Entropy(Sv1) + (|Sv2| / S) * Entropy(Sv2) + ...]
    • Chia dữ liệu theo thuộc tính A → thành nhiều nhóm (ví dụ “Weather” → Sunny/Rain/Windy…)
    • Tính entropy của từng nhóm.
    • Lấy trung bình theo trọng số số lượng mẫu.
Information Gain (độ tăng thông tin):
Sự giảm hỗn loạn khi chia theo thuộc tính. Thuộc tính có Information Gain cao nhất → chọn làm node.
Gain(S,A)=Entropy(S)−EntropyA(S)
    • Gain = mức giảm độ hỗn loạn khi chia bằng A.
    • A càng làm tập “thuần” hơn → Gain càng lớn → được chọn.
Bài tập
Demo cây quyết định với thuật toán id3