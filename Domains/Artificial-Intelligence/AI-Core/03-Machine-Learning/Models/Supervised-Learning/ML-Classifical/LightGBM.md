- [LightGBM](#lightgbm)
  - [GOSS (Gradient-based One-Side Sampling - cách lấy mẫu dữ liệu thông minh trong LightGBM)](#goss-gradient-based-one-side-sampling---cách-lấy-mẫu-dữ-liệu-thông-minh-trong-lightgbm)
- [Practices](#practices)
  - [Demo Pipeline của LightGBM bằng ý tưởng](#demo-pipeline-của-lightgbm-bằng-ý-tưởng)
---
# LightGBM 
```bash
LightGBM - Light Gradient Boosting Machine là một model machine learning. 
    Cụ thể hơn nó là dạng ensemble model - kết hợp nhiều mô hình nhỏ

Nó cùng “họ” XGBoost, CatBoost và được huấn luyện theo kiểu boosting
```
**[Link giới thiệu thuật toán boosting](./Base.md#Boosting)**
**Lịch sử ra đời**
```bash
- Do Microsoft phát triển bắt đầu khoảng từ năm 2016
- Paper chính công bố năm 2017 tại NeurIPS
```
**Paper nên đọc**
```bash
1. “LightGBM: A Highly Efficient Gradient Boosting Decision Tree” (2017)
```
**LightGBM ra đời để giải quyết vấn đề gì?**
```bash
Trước LightGBM đã có:
    - Gradient Boosting (cổ điển)
    - XGBoost (rất nổi tiếng)

Nhưng vấn đề:
    ❌ Train chậm
    ❌ Dataset lớn là “toang”
    ❌ Feature nhiều → cực kỳ tốn tài nguyên
→ LightGBM được tạo ra để:
    🚀 train nhanh hơn
    💾 ít tốn RAM hơn
    📊 scale được dữ liệu lớn
```
**So sánh Decision Tree, Random Forest, LightGBM**
```bash
| Loại     | Ví dụ         | Ý tưởng                             |
| -------- | ------------- | ----------------------------------- |
| Tree đơn | Decision Tree | 1 cây duy nhất                      |
| Ensemble | Random Forest | nhiều cây, train độc lập            |
| Boosting | LightGBM      | nhiều cây, train tuần tự để sửa lỗi |
```
**LightGBM khác XGBoost ở điểm nào?**
```bash
1. XGBoost: Level-wise growth
    Giả sử ban đầu cây chỉ có một node gốc:

            Root
    Sau lần tách đầu tiên:
            Root
           /    \
          A      B

    XGBoost sẽ phát triển theo từng tầng (level).
        Nghĩa là trước khi xuống sâu hơn, nó sẽ tách tất cả node ở cùng tầng.
            Ví dụ:
                Bước 1
                        Root
                       /    \
                      A      B
                Bước 2: Tách cả A và B
                       Root
                      /    \
                     A      B
                    / \    / \
                  A1  A2 B1  B2
                Bước 3: Tách tiếp tất cả node tầng dưới
                         Root
                       /      \
                      A        B
                    /  \      /  \
                  A1   A2   B1   B2
                 / \   / \  / \  / \
    
    Ưu điểm
        - Cây khá cân bằng:
                 O
               /   \
              O     O
             / \   / \
            O   O O   O
            => ít nguy cơ overfit hơn
    
    Nhược điểm
        - Có nhiều node không đáng để tách nhưng vẫn phải xét.
            Ví dụ:
                   Root
                  /    \
                 A      B
                Giả sử:
                    - Tách A giúp giảm loss 100 điểm
                    - Tách B chỉ giảm loss 1 điểm
                    - XGBoost vẫn phải tách cả A lẫn B vì chúng cùng tầng.

2. LightGBM: Leaf-wise growth
    LightGBM không quan tâm tầng.
        Nó luôn hỏi: "Trong toàn bộ cây hiện tại, lá nào nếu tách sẽ làm giảm loss nhiều nhất?" => Sau đó chỉ tách lá đó.
    
    Ví dụ
        Ban đầu: 
            Root
        Tách lần đầu:
                Root
               /    \
              A      B
        Giả sử:
            - Gain(A) = 100
            - Gain(B) = 5
            LightGBM chọn A.
        Kết quả:
                Root
               /    \
              A      B
             / \
           A1  A2
        Lần tiếp theo:
            - Gain(A1)=80
            - Gain(A2)=30
            - Gain(B)=5
        LightGBM lại chọn A1.
                Root
               /    \
              A      B
             / \
           A1  A2
          / \
        A11 A12
```
**Tại sao dễ overfit hơn?**
```bash
Giả sử dữ liệu chỉ có 100 mẫu.

LightGBM có thể tạo cây như:
            Root
           /
          O
         /
        O
       /
      O
     /
    O

Mỗi lần tách chỉ tập trung vào một vùng nhỏ của dữ liệu.
    Cuối cùng có thể xuất hiện lá chỉ chứa:
        3 mẫu hoặc 1 mẫu
    Lúc này cây đang học thuộc dữ liệu train.
=> Đó chính là overfitting.
```
**Ý tưởng cốt lõi của model LightGBM**
```bash
Giả sử:
    - Model đầu tiên dự đoán sai nhiều
    - Model thứ 2 học lỗi của model 1
    - Model thứ 3 học tiếp lỗi
    => Cứ thế cộng dồn lại → model mạnh dần => Đây gọi là Gradient Boosting
```
**Dataset**
```bash
1. https://archive.ics.uci.edu/dataset/321/electricityloaddiagrams20112014
```
## GOSS (Gradient-based One-Side Sampling - cách lấy mẫu dữ liệu thông minh trong LightGBM)
```bash
Thay vì dùng toàn bộ data, nó:
    + Giữ lại những điểm có gradient lớn (quan trọng)
    + Lấy ngẫu nhiên một phần gradient nhỏ (ít quan trọng)
➡️ Giảm data nhưng vẫn giữ thông tin chính

Gradient = “mức độ sai”
    + |gradient| lớn → model đang dự đoán rất sai → rất quan trọng
    + |gradient| nhỏ → model dự đoán gần đúng → ít quan trọng
    👉 Ý tưởng: Không cần học lại những điểm đã gần đúng
```
**Ex**
```bash
Giả sử bạn có 8 sample:
| ID | y   | y_pred | gradient = y - y_pred |
| -- | --- | ------ | --------------------- |
| 1  | 100 | 130    | -30                   |
| 2  | 120 | 130    | -10                   |
| 3  | 150 | 130    | +20                   |
| 4  | 170 | 130    | +40                   |
| 5  | 140 | 130    | +10                   |
| 6  | 135 | 130    | +5                    |
| 7  | 128 | 130    | -2                    |
| 8  | 132 | 130    | +2                    |
```
```bash
⚡ Bước 1: Chọn top gradient lớn
    - Giả sử: Giữ top 50% gradient lớn nhất 👉 Sắp xếp theo |gradient|:
        | ID | gradient | |gradient| |
        |----|----------|------------|
        | 4  | +40      | 40         |
        | 1  | -30      | 30         |
        | 3  | +20      | 20         |
        | 2  | -10      | 10         |
        | ...| ...      | ...        |
        👉 Lấy 4 điểm lớn nhất: ID: 4, 1, 3, 2

🎲 Bước 2: Sample phần còn lại
    - Phần còn lại: ID: 5, 6, 7, 8 👉 Lấy ngẫu nhiên 50%: ID: 5, 7
    - 📦 Dataset sau GOSS Final data: 4, 1, 3, 2, 5, 7
    👉 Tức là:
        + Không dùng toàn bộ data
        + Nhưng vẫn giữ:
        + tất cả điểm quan trọng
        + một ít điểm “ít quan trọng”
    - ⚠️ Vấn đề: bị lệch phân phối
        + Nếu bạn dừng ở đây → sai ❌ Vì:
            - Bạn giữ nhiều điểm gradient lớn
            - Ít điểm gradient nhỏ
            ➡️ Dataset bị bias

Bước 3: Re-weight (cực quan trọng)
    - LightGBM sẽ tăng trọng số cho phần sample nhỏ
    👉 Ví dụ bạn giữ:
        + 100% gradient lớn
        + 50% gradient nhỏ
        ➡️ thì: các điểm gradient nhỏ sẽ được nhân weight ≈ 2

🌳 Bước 4: Dùng data này để build tree
    - LightGBM sẽ:
        + tính histogram
        + split
        + grow tree
    👉 Nhưng chỉ trên subset data đã chọn
```
# Practices
## Demo Pipeline của LightGBM bằng ý tưởng
**Bài toán dự đoán giá nhà (regression)**
```bash
Dataset đơn giản:
| ID | Diện tích (m²) | Số phòng | Giá thật (y) |
| -- | -------------- | -------- | ------------ |
| 1  | 50             | 2        | 100          |
| 2  | 60             | 2        | 120          |
| 3  | 70             | 3        | 150          |
| 4  | 80             | 3        | 170          |
```
**Bước 0: Khởi tạo dự đoán ban đầu**
```bash
LightGBM chưa có cây nào nên phải dự đoán một giá trị chung cho toàn bộ dữ liệu.
    Với bài toán Regression (MSE), giá trị này chính là **trung bình của y**.

y_pred0 = (100+120+150+170)/4=135
=> Tất cả sample ban đầu: y_pred = [135, 135, 135, 135]

Ban đầu:
    | ID | y | y_pred |
    |----|---|--------|
    |1   |100|135     |
    |2   |120|135     |
    |3   |150|135     |
    |4   |170|135     |

💡 Ý nghĩa:
    Model hiện tại chỉ biết đoán:
        > "Tôi chưa học gì cả nên mọi căn nhà đều có giá 135."
```
**Bước 1: Tính sai số - Pseudo Residual**
```bash
LightGBM cần biết mình đang dự đoán sai bao nhiêu.

Ta tính:
    residual = y - y_pred
    
    | ID | y   | y_pred | residual |
    | -- | --- | ------ | -------- |
    | 1  | 100 | 135    | -35      |
    | 2  | 120 | 135    | -15      |
    | 3  | 150 | 135    | +15      |
    | 4  | 170 | 135    | +35      |
        + âm → dự đoán quá cao
        + dương → dự đoán quá thấp
```
**Bước 2: GOSS (Gradient-based One-Side Sampling)**
```bash
Thông thường Gradient Boosting sẽ dùng toàn bộ dữ liệu để train cây.
    Nhưng LightGBM muốn nhanh hơn. => Nó quan sát residual:
        Các residual có độ lớn lớn nhất thường là những điểm model đang sai nhiều nhất

        Giả sử: 
            + giữ top gradient lớn: 35, -35
            + sample thêm 1 điểm nhỏ: -15
        ➡️ Các sample dùng để train tree: ID: 1, 2, 4

💡 Trong LightGBM thật:
    - giữ toàn bộ residual lớn
    - lấy ngẫu nhiên một phần residual nhỏ
    - các residual nhỏ được tăng trọng số để tránh bias.
=> Mục tiêu là giảm số lượng dữ liệu nhưng vẫn giữ thông tin quan trọng.

💡 Đây là cách LightGBM giảm data nhưng vẫn giữ thông tin quan trọng.
```
**Bước 3: Histogram-based Tree**
```bash
Dataset (nhắc lại):
    | ID | Diện tích | gradient |
    | -- | --------- | -------- |
    | 1  | 50        | -35      |
    | 2  | 60        | -15      |
    | 3  | 70        | +15      |
    | 4  | 80        | +35      |

⚡ 3.1 Binning feature (Chia Feature thành các Bin)
    Thay vì xét từng giá trị:
        50
        60
        70
        80
    
    LightGBM chia thành các nhóm (bin).
        Ví dụ:
            | Bin | Range |
            | --- | ----- |
            | B1  | <=60  |
            | B2  | >60   |
            
        Mapping:
            | ID | Diện tích | Bin |
            |----|-----------|-----|
            |1   |50         |B1   |
            |2   |60         |B1   |
            |3   |70         |B2   |
            |4   |80         |B2   |
        
    💡 Thực tế LightGBM dùng Approximate Quantile để chia bin rất nhanh ngay từ đầu.
            Việc chia bin **chỉ dựa vào giá trị feature**, không dựa vào residual.


            LightGBM dùng quantile-based binning để chia bin
                - Hiểu đơn giản
                    + Nó cố gắng chia sao cho: mỗi bin có số lượng data gần bằng nhau
                    + 📊 Ví dụ: Giả sử feature “diện tích”: [50, 60, 70, 80, 90, 100]. Bạn muốn chia 3 bin:
                        👉 LightGBM sẽ sort: [50, 60, 70, 80, 90, 100]
                        👉 chia đều:
                            Bin	Range
                            B1	50–60
                            B2	70–80
                            B3	90–100
                        💡 Đây gọi là quantile binning
                ⚠️ Nhưng thực tế còn tinh vi hơn
                    + LightGBM không làm naive như trên, nó dùng:
                        - approximate quantile (rất nhanh)
                    👉 vì:
                        dataset có thể hàng triệu dòng
                        không thể sort full mỗi lần
                
                🔥 Một twist quan trọng 
                    👉 LightGBM KHÔNG chỉ dựa vào feature. Nó còn tối ưu cho: 
                        gradient distribution ➡️ nghĩa là: bin nào có gradient “khác biệt” sẽ được giữ rõ hơn
        
3.2 Gom Residual theo từng Bin
    Sau khi đã biết mỗi sample thuộc bin nào, LightGBM cộng residual trong từng bin.
            | Bin | Samples | Tổng residual     |
            | --- | ------- | ----------------- |
            | B1  | ID 1,2  | -35 + (-15) = -50 |
            | B2  | ID 3,4  | +15 + 35 = +50    |
            
        (LightGBM thật còn có Hessian H). Với MSE: Hessian ≈ 1 cho mỗi điểm 👉 nên:
            | Bin | H (số mẫu) |
            | --- | ---------- |
            | B1  | 2          |
            | B2  | 2          |
    
3.3 Tính Gain
    LightGBM thử chia cây tại các vị trí khác nhau.
            
    Ví dụ:
        Split: Diện tích <= 60

        Nếu sau khi chia:
            - Bên trái: toàn residual âm
            - Bên phải: toàn residual dương

            thì nghĩa là:
                - nhóm bên trái đang bị dự đoán quá cao
                - nhóm bên phải đang bị dự đoán quá thấp
            => Đây là cách chia rất tốt.

            LightGBM tính một giá trị gọi là **Gain**.
                Gain càng lớn → Split càng tốt. => Nó sẽ chọn split có Gain lớn nhất.

    Công thức Gain (đơn giản hóa): Gain = GL**2/HL + GR**2/HR
        + GL: tổng gradient bên trái
        + HL: tổng hessian bên trái
    - Thay số vào
        + Left (B1): GL = −50, HL = 2
        + Right (B2): GR = 50, HR = 2
    - Tính: Gain=(−50)^2/2+(50)^2/2 = 2500/2+2500/2 =1250+1250=2500
        👉 Nếu:
            + bên trái toàn gradient âm
            + bên phải toàn gradient dương
        ➡️ nghĩa là: model đang sai theo 2 hướng hoàn toàn khác nhau 👉 Split này RẤT TỐT (Gain càng lớn càng tốt)
```
**Bước 4: Xây cây theo Leaf-wise** 
```bash
Giả sử cây đầu tiên là:
      Root
    Area <=60
    /       \
Leaf1      Leaf2

Khác với XGBoost thường phát triển cân bằng,
    LightGBM luôn chọn:
        > Leaf nào giúp giảm Loss nhiều nhất thì tiếp tục split leaf đó.
=> Đây gọi là **Leaf-wise Growth**.
```
**Bước 5: Tính giá trị của từng Leaf**
```bash
Sau khi cây hoàn thành, mỗi leaf sẽ học một giá trị để sửa prediction.
    Ví dụ:
        Leaf1: ID1, ID2
            Residual:
                -35
                -15
            Trung bình: -25

        Leaf2: ID3, ID4
            Residual:
                15
                35
            Trung bình: 25

💡 Thực tế LightGBM dùng:
    leaf_value = -sum(gradient)/(sum(hessian)+λ)
        Nhưng với Regression đơn giản có thể hiểu gần giống như trung bình residual.
```
**Bước 6: Update prediction**
```bash
Giả sử: 
    learning rate = 0.1
    Prediction mới: prediction_new = prediction_old + learning_rate × leaf_value
        ID	y_pred_cũ	leaf	update	y_pred_mới
        1	135	        Leaf1	-2.5	132.5
        2	135	        Leaf1	-2.5	132.5
        3	135	        Leaf2	+3.5	138.5
        4	135	        Leaf2	+3.5	138.5
    
Công thức: ynew = yold + η⋅leaf_value
```
**Bước 7: Lặp lại**
```bash
LightGBM sẽ:
    + Tính gradient mới
    + Build cây mới
    + Update tiếp

➡️ Sau nhiều vòng → model hội tụ
```