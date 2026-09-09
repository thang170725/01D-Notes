- [<<Back](../Base.md)

- [Practices>>](Practices.md)

- [RNN Introduction (Recurrent Neural Network là một kiến trúc mạng neural dùng để xử lý dữ liệu tuần tự (sequential data))](#rnn-introduction-recurrent-neural-network-là-một-kiến-trúc-mạng-neural-dùng-để-xử-lý-dữ-liệu-tuần-tự-sequential-data)
---
# RNN Introduction (Recurrent Neural Network là một kiến trúc mạng neural dùng để xử lý dữ liệu tuần tự (sequential data))
```bash
RNN nhận một chuỗi input và xử lý nó từng phần tử theo thứ tự, đồng thời mang theo một "memory" từ bước trước sang bước sau.
```
**RNN thực sự giải quyết vấn đề gì**
```bash
Nó giải quyết một vấn đề rất quan trọng:
    Làm thế nào để xử lý dữ liệu có thứ tự mà thông tin ở quá khứ ảnh hưởng đến hiện tại?
```
**Ý tưởng**
```bash
Thông tin ở bước t−1 sẽ được kết hợp với đầu vào ở bước t để tạo ra trạng thái mới.

Điều này rất phù hợp với: 
    - Chuỗi văn bản
    - Dữ liệu thời gian (time series)
    - Chuỗi tín hiệu âm thanh, video, …
```
**Vấn đề**
```bash
- RNN quên rất nhanh.
- Không nhớ được thông tin xa.
- Bị vanishing gradient khi chuỗi dài.
- Bạn đọc câu: "Tôi ăn cơm lúc 7h sáng, và đến chiều thì tôi đói." 
    + RNN có thể không nhớ phần trước 7h sáng vì quá xa → mất ngữ cảnh 

→ RNN phù hợp với chuỗi ngắn, hoặc tác vụ đơn giản.
```
**Kiến trúc RNN**
```bash
- Một RNN đơn giản có 3 tham số chính:
Wxh  (input → hidden)
Whh  (hidden → hidden)
Why  (hidden → output)

- Giả sử:
input size = 8
hidden size = 4
output size = 8
```
**Công thức RNN**
```bash
- Hidden state: ℎ𝑡 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥𝑡 + 𝑊ℎℎ.ℎ𝑡−1 + 𝑏ℎ)
- Output: 𝑦𝑡 = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑊ℎ𝑦.ℎ𝑡 + 𝑏𝑦)
```
**Workflow RNN**
[Worfflow RNN](Practices.md#mô-tả-work-flow-của-rnn-cho-bài-toán-dự-đoán-từ-tiếp-theo)
# CRNN Introduction
```bash
CRNN = Convolutional Recurrent Neural Network — tức là kiến trúc kết hợp CNN + RNN.

Điểm quan trọng nhất là:
    CNN chịu trách nhiệm “nhìn/ trích xuất đặc trưng”, còn RNN chịu trách nhiệm “đọc chuỗi theo thứ tự”.

    Vì vậy CRNN rất hay dùng cho OCR, nhận dạng chữ trong ảnh, handwriting recognition, speech recognition...
```
**RNN bình thường là gì?**
```bash
Ví dụ bạn có một chuỗi: I → love → AI

RNN đọc lần lượt:
    x1        x2        x3
    ↓         ↓         ↓
    RNN ───→ RNN ───→ RNN
    ↓         ↓         ↓
    h1        h2        h3

Tại thời điểm t:

$$ h_t = f(x_t, h_{t-1}) $$

Nó lấy:

x_t: input hiện tại
h_{t-1}: thông tin từ quá khứ
tạo ra h_t: trạng thái hiện tại

Ví dụ:

"I" → RNN → h1
"love" → RNN → h2
"AI" → RNN → h3

RNN rất phù hợp khi input đã là sequence.

Ví dụ:

[10, 20, 30, 40, 50]

hoặc:

["I", "love", "AI"]
2. Nhưng ảnh thì sao?

Đây chính là chỗ CRNN xuất hiện.

Giả sử có ảnh:

5
+-----------------------+
|                       |
|    HELLO WORLD        |
|                       |
+-----------------------+

Ảnh này là một ma trận:

Height × Width × Channels

Ví dụ:

32 × 200 × 1

RNN không trực tiếp hiểu tốt ảnh 2D.

Ta cần CNN trước.
```
**CRNN hoạt động như thế nào?**
```bash
Kiến trúc cơ bản: Image -> CNN -> Feature Map -> Convert thành sequence -> RNN / BiLSTM -> CTC / Decoder -> "HELLO"

Nói cách khác: CNN → RNN # Đó chính là CRNN.
```
4. CNN làm gì?

CNN nhìn ảnh và tìm đặc trưng.

Ví dụ ảnh:

H E L L O

CNN có thể biến nó thành feature map:

       Feature Map

      width →
   ┌──┬──┬──┬──┬──┬──┐
   │  │  │  │  │  │  │
   ├──┼──┼──┼──┼──┼──┤
   │  │  │  │  │  │  │
   ├──┼──┼──┼──┼──┼──┤
   │  │  │  │  │  │  │
   └──┴──┴──┴──┴──┴──┘
    ↓  ↓  ↓  ↓  ↓  ↓
    t1 t2 t3 t4 t5 t6

Mỗi cột của feature map có thể được xem như một timestep.

Ví dụ:

Feature map:

H   E   L   L   O
↓   ↓   ↓   ↓   ↓
t1  t2  t3  t4  t5

Sau đó đưa vào RNN:

t1 → RNN → h1
           ↓
t2 → RNN → h2
           ↓
t3 → RNN → h3
           ↓
t4 → RNN → h4
           ↓
t5 → RNN → h5

RNN học quan hệ giữa các vùng ảnh theo chiều ngang.

5. Đây là điểm khác biệt cực kỳ quan trọng
RNN bình thường

Input đã là sequence:

x1 → x2 → x3 → x4

Ví dụ:

The → cat → is → sleeping

RNN xử lý trực tiếp.

CRNN

Input ban đầu là ảnh:

Image
  ↓
CNN
  ↓
Feature map
  ↓
Sequence
  ↓
RNN

CNN biến:

2D image

thành:

sequence of visual features

rồi RNN xử lý sequence đó.

6. Ví dụ OCR

Giả sử ảnh:

┌──────────────────────┐
│      C A T           │
└──────────────────────┘

CNN có thể tạo:

Feature:

f1  f2  f3  f4  f5  f6
↓   ↓   ↓   ↓   ↓   ↓

Trong đó mỗi fi chứa thông tin về một vùng ảnh.

RNN đọc:

f1 → f2 → f3 → f4 → f5 → f6

và dự đoán:

C → A → T

Thường kiến trúc thực tế còn có BiLSTM:

CNN
 │
 ▼
Feature Sequence
 │
 ▼
BiLSTM
 │
 ▼
CTC
 │
 ▼
CAT
7. Tại sao không dùng CNN thôi?

CNN rất giỏi nhận diện spatial features:

edge
curve
shape
texture
...

Nhưng OCR còn cần hiểu thứ tự.

Ví dụ:

C A T

khác:

T A C

CNN có thể nhận diện các ký tự, nhưng cần một cơ chế sequence để model hiểu:

C đứng trước A
A đứng trước T

RNN đảm nhận phần này.

8. Tại sao không dùng RNN thôi?

Ngược lại:

RNN rất giỏi sequence:

x1 → x2 → x3 → x4

nhưng ảnh là:

H × W × C

Nếu đưa raw pixel trực tiếp vào RNN thì rất không hiệu quả.

CNN trước giúp:

raw pixels
    ↓
visual features

sau đó RNN chỉ cần xử lý:

visual feature sequence
9. Một cách nhìn rất hay

Bạn có thể nhớ CRNN bằng câu:

CNN biến ảnh thành “ngôn ngữ” mà RNN có thể đọc.

Ví dụ:

Ảnh
 ↓
CNN
 ↓
[feature₁, feature₂, feature₃, feature₄, ...]
                         ↓
                     sequence
                         ↓
                       RNN
                         ↓
                    character sequence

Đây chính là tư tưởng cốt lõi.

10. So sánh
	RNN	CRNN
Input	Sequence	Image
CNN	❌	✅
RNN	✅	✅
Xử lý spatial feature	Không tốt	CNN làm
Xử lý sequence	✅	RNN làm
OCR	Có thể nhưng không tự nhiên	Rất phù hợp
Speech	Có	Có thể
Text recognition	Có	Rất phổ biến
11. Và có một chi tiết rất đáng học: CTC

Nếu bạn đang học seq2seq/RNN, CRNN + CTC (Connectionist Temporal Classification) là một ví dụ cực hay.

Bởi vì ảnh:

[ảnh chữ "HELLO"]

không nhất thiết biết chính xác:

pixel nào = H
pixel nào = E
pixel nào = L
...

Ta chỉ có label:

HELLO

CRNN + CTC có thể học mapping:

Image
 ↓
CNN
 ↓
sequence
 ↓
BiLSTM
 ↓
CTC
 ↓
HELLO

mà không cần bounding box cho từng ký tự.

Đây là một trong những lý do CRNN từng rất quan trọng trong OCR.

Nếu mục tiêu của bạn là hiểu sâu RNN/Seq2Seq chứ không chỉ dùng model, thì mình khuyên học CRNN theo thứ tự:

RNN
 ↓
LSTM
 ↓
BiLSTM
 ↓
CNN feature extraction
 ↓
CRNN
 ↓
CTC
 ↓
CRNN OCR

Đặc biệt CTC sẽ là phần rất đáng học, vì nó giúp bạn hiểu một ý tưởng quan trọng: input sequence và output sequence có thể có độ dài khác nhau mà không cần align thủ công từng timestep.

là sao chưa hiểu đoạn này Feature Map -> Convert thành sequence làm sao mà convert được vì feature map toàn số mà kiểu như 224x224x64 chẳng hạn làm sao convert được thành kiểu hello, chưa hình dùng được

Đúng, câu hỏi của bạn chạm đúng chỗ dễ hiểu sai nhất của CRNN. Và bạn đang hiểu đúng một phần: nếu thật sự chỉ lấy 1 giá trị trong 256 channel thì đúng là vô nghĩa. Nhưng CRNN không làm như vậy.

Điểm cần sửa trong cách hình dung của bạn là:

Một timestep không phải là một số. Một timestep là một vector chứa toàn bộ thông tin của các channel và thường cả chiều height.

1. Quay lại tensor 14 × 28 × 512

Giả sử CNN cho ra:

H = 14
W = 28
C = 512

Ta có:

Feature Map = [14, 28, 512]

Hãy cố định width = 1.

Khi đó ta lấy:

[:, width=1, :]

Kết quả có kích thước:

14 × 512

Không phải 14 × 1.

Tức là ta giữ nguyên:

toàn bộ 14 giá trị theo height
toàn bộ 512 channel
2. Hãy nhìn một cột đúng nghĩa

Ta có:

                  WIDTH
          1        2        3        4
       ┌────────┬────────┬────────┬────────┐
H = 1  │ 512 số │ 512 số │ 512 số │ 512 số │
H = 2  │ 512 số │ 512 số │ 512 số │ 512 số │
H = 3  │ 512 số │ 512 số │ 512 số │ 512 số │
H = 4  │ 512 số │ 512 số │ 512 số │ 512 số │
...    │  ...   │  ...   │  ...   │  ...   │
H = 14 │ 512 số │ 512 số │ 512 số │ 512 số │
       └────────┴────────┴────────┴────────┘

Một cột width = 1 thực chất là:

┌───────────────────┐
│ 512 features      │
├───────────────────┤
│ 512 features      │
├───────────────────┤
│ 512 features      │
├───────────────────┤
│       ...         │
├───────────────────┤
│ 512 features      │
└───────────────────┘
       14 rows

Nó có:

14 × 512 = 7168 số
3. Vậy tại sao lại gọi nó là 1 timestep?

Đây mới là ý tưởng quan trọng.

Ta có:

width = 1

→ coi toàn bộ vùng đó là một timestep.

Sau đó:

width = 2

→ timestep thứ 2.

width = 3

→ timestep thứ 3.

...

width = 28

→ timestep thứ 28.

Nên ta biến:

14 × 28 × 512

thành conceptually:

timestep 1 = 14 × 512 numbers
timestep 2 = 14 × 512 numbers
timestep 3 = 14 × 512 numbers
...
timestep 28 = 14 × 512 numbers

Sau đó thường flatten mỗi timestep:

14 × 512

thành:

7168

Vậy RNN nhìn thấy:

x1 = vector 7168 chiều
x2 = vector 7168 chiều
x3 = vector 7168 chiều
...
x28 = vector 7168 chiều

Đây mới là sequence.

4. Bạn đang hình dung nhầm "channel"

Bạn nói:

"lấy cột 1 thì 256 channel sẽ lấy đúng được 1 giá trị channel đầu"

Không phải.

Giả sử:

Feature Map = 32 × 100 × 256

Tại:

width = 1
height = 1

ta có:

[ c1, c2, c3, ..., c256 ]

Đây là 256 channel của vị trí đó.

Tại:

width = 1
height = 2

lại có:

[ c1, c2, c3, ..., c256 ]

...

Tại:

width = 1
height = 32

lại có:

[ c1, c2, c3, ..., c256 ]

Vậy cả cột:

width = 1

là:

[
  [c1, c2, ..., c256],   ← height 1
  [c1, c2, ..., c256],   ← height 2
  [c1, c2, ..., c256],   ← height 3
  ...
  [c1, c2, ..., c256]    ← height 32
]

Tức:

32 × 256

rồi flatten:

8192 numbers

Không hề mất 255 channel còn lại.

5. Nhưng câu hỏi sâu hơn của bạn mới thực sự hay

Bạn có thể hỏi:

"OK, nhưng tại sao gom cả 14 height × 512 channel vào một timestep lại có ý nghĩa?"

Đây là câu hỏi đúng.

Bởi vì CNN đã làm rất nhiều việc trước đó.

CNN không còn cho chúng ta raw pixel nữa.

Ví dụ:

raw image
224 × 224 × 3

sau nhiều convolution/pooling:

14 × 28 × 512

512 channel có thể được hiểu một cách trực giác là 512 loại feature khác nhau mà CNN học được.

Ví dụ rất đơn giản hóa:

channel 1   → edge
channel 2   → vertical stroke
channel 3   → horizontal stroke
channel 4   → curve
...
channel 512 → complex visual pattern

Không nên hiểu đúng literal rằng channel 17 chắc chắn là "vertical stroke"; model tự học representation. Nhưng trực giác này hữu ích.

6. Bây giờ hãy tưởng tượng ảnh chữ HELLO

Ảnh:

H        E        L        L        O
│        │        │        │        │
▼        ▼        ▼        ▼        ▼

┌───────────────────────────────────────────┐
│                                           │
│              HELLO                        │
│                                           │
└───────────────────────────────────────────┘

CNN tạo feature map.

Theo chiều width:

→ → → → → → → → → → → → → → →

Các vùng khác nhau của width chứa thông tin khác nhau:

       H          E          L       L       O
       ↓          ↓          ↓       ↓       ↓
     width       width      width   width   width

Cho nên ta muốn:

x1 → x2 → x3 → x4 → ... → x28

để RNN có thể đọc:

trái → phải
7. Nhưng RNN có thực sự hiểu từng ký tự không?

Không.

Đây cũng là một điểm rất quan trọng.

Ví dụ:

x1 = [7168 numbers]

không có nghĩa:

x1 = "H"

Có thể:

x1 → một phần của H
x2 → phần còn lại của H
x3 → khoảng giữa H và E
x4 → một phần của E
...

Ranh giới ký tự không nhất thiết trùng với timestep.

Đây chính là một trong những lý do CTC hữu ích.

8. Và đây là lý do CRNN rất đẹp

Bạn có thể nhìn toàn bộ quá trình như thế này:

CNN
ẢNH
 ↓
tìm visual features
 ↓
Feature Map
Chuyển thành sequence
Feature Map

      width →
 ┌──┬──┬──┬──┬──┬──┐
 │  │  │  │  │  │  │
 │  │  │  │  │  │  │
 │  │  │  │  │  │  │
 └──┴──┴──┴──┴──┴──┘
  ↓  ↓  ↓  ↓  ↓  ↓
 x1 x2 x3 x4 x5 x6

Mỗi x là một vector lớn, không phải một scalar.

RNN
x1 → x2 → x3 → x4 → x5 → ...

RNN học quan hệ:

feature ở bên trái
        ↓
feature ở giữa
        ↓
feature ở bên phải
Linear + CTC
hidden states
      ↓
character probabilities
      ↓
H H blank E E blank L L L ...
      ↓
    "HELLO"
9. Có một điểm nữa: trong CRNN người ta thường giảm height về 1

Đây là chỗ mình muốn chỉnh lại câu trả lời trước để bạn khỏi bị rối.

Trong nhiều kiến trúc CRNN OCR, CNN được thiết kế sao cho cuối CNN feature map có dạng kiểu:

1 × W × C

chứ không phải:

H × W × C

Ví dụ:

CNN output:

1 × 28 × 512

Lúc này mọi chuyện cực kỳ dễ:

       width
       ↓
┌────┬────┬────┬────┬────┐
│512 │512 │512 │512 │512 │
└────┴────┴────┴────┴────┘
  ↓    ↓    ↓    ↓    ↓
 x1   x2   x3   x4   x5

Mỗi timestep chỉ còn:

512 numbers

và sequence là:

[x1, x2, x3, ..., x28]

với:

x1.shape = 512
x2.shape = 512
...

Đây có lẽ là hình ảnh bạn đang thiếu để hiểu CRNN.

Tóm lại

Bạn vừa phát hiện ra một điểm rất quan trọng:

Không phải "lấy một cột = lấy một channel".

Mà là:

Feature map
H × W × C

        ↓ lấy theo width

W timesteps

mỗi timestep:
H × C features

        ↓ flatten

H*C features

        ↓

RNN

Và trong nhiều CRNN OCR:

CNN
 ↓
1 × W × C
 ↓
W timesteps × C features
 ↓
BiLSTM

Nếu bạn muốn hiểu tới tận tensor level, cách tốt nhất tiếp theo là lấy một ví dụ 2×4×3 và mình sẽ vẽ từng ô số cụ thể rồi thực hiện permute + reshape bằng tay. Lúc đó bạn sẽ thấy chính xác tại sao W trở thành sequence length và không một channel nào bị "cắt mất".

nhưng ví dụ tất cả thông tin của channel 1 nó phân bổ vào tất cả cell mà. ví dụ vector chanel 1 = 
                  WIDTH 
          1        2        3        4 
       ┌────────┬────────┬────────┬────────┐ 
H = 1  │ lấy số đầu tiên của 512 số │ lấy số đầu tiên 512 số │ 512 số │ 512 số │ 
H = 2  │ 512 số │ 512 số │ 512 số │ 512 số │ 
H = 3  │ 512 số │ 512 số │ 512 số │ 512 số │ 
H = 4  │ 512 số │ 512 số │ 512 số │ 512 số │ 
...    │  ...   │  ...   │  ...   │  ...   │ 
H = 14 │ 512 số │ 512 số │ 512 số │ 512 số │ 
       └────────┴────────┴────────┴────────┘"" sau đó gộp hết các số đầu tiên thì mới ra vector channel 1 chứ, tương tự với channel 2, 3, 4 chứ có phải ở ô width=1, height=1 giá trị là vector channel = 1 đâu

Đúng — giờ mình hiểu chính xác bạn đang vướng ở đâu. Và thực ra bạn đang phân biệt đúng giữa:

channel
spatial cell (height, width)
vector tại một cell

Chỗ trước mình diễn đạt "mỗi cell có 512 số" là đúng, nhưng ví dụ channel 1 của bạn đang đặt ra một vấn đề rất hay.

Quan trọng: channel 1 KHÔNG phải là một vector duy nhất

Nếu tensor là:

H × W × C = 14 × 28 × 512

thì channel 1 chính là cả một ma trận:

14 × 28

Ví dụ:

Channel 1:

        W1   W2   W3   W4
H1      a11  a12  a13  a14
H2      a21  a22  a23  a24
H3      a31  a32  a33  a34
H4      a41  a42  a43  a44

Channel 2:

        W1   W2   W3   W4
H1      b11  b12  b13  b14
H2      b21  b22  b23  b24
...

...

Channel 512:

        W1   W2   W3   W4
H1      z11  z12  z13  z14
...

Bạn nói đúng: thông tin của channel 1 được phân bố trên tất cả các spatial cell.

Nhưng có một điểm bạn đang gọi nhầm là "vector channel 1"

Bạn nói:

"sau đó gộp hết các số đầu tiên thì mới ra vector channel 1"

Nếu bạn lấy toàn bộ channel 1 thì:

14 × 28

số đó tạo thành feature map của channel 1, chứ không phải một "vector channel" theo nghĩa của CNN.

Ví dụ:

C1 =

a11 a12 a13 ... a1,28
a21 a22 a23 ... a2,28
...
a14,1 ...       a14,28

Nó là một 2D feature map.

Còn một cell (H=1, W=1) là gì?

Đây mới là mấu chốt.

Tại một spatial position:

(H=1, W=1)

ta có:

[
  C1_value,
  C2_value,
  C3_value,
  ...
  C512_value
]

Tức là:

(H=1, W=1) → vector 512 chiều

Ví dụ:

(1,1) = [
    0.12,    ← channel 1
    0.87,    ← channel 2
    -0.31,   ← channel 3
    ...
    0.45     ← channel 512
]

Không phải:

(1,1) → channel 1

Mà là:

(1,1) → tất cả 512 channels
Đây chính là điểm bạn vừa nói

Bạn đang nhìn tensor theo channel trước:

Channel 1
    ↓
14 × 28

Channel 2
    ↓
14 × 28

...

Channel 512
    ↓
14 × 28

Cách này hoàn toàn đúng.

Nhưng khi CRNN muốn tạo sequence, nó thường nhìn tensor theo spatial position trước:

Cell (1,1)
    ↓
512 numbers

Cell (2,1)
    ↓
512 numbers

Cell (3,1)
    ↓
512 numbers

...

Tức là hai cách nhìn khác nhau trên cùng một tensor.

Ví dụ cực nhỏ: 2 × 3 × 4

Để bỏ hết số 512 cho dễ nhìn.

Ta có:

H = 2
W = 3
C = 4

Có 4 channels:

C1:
┌────┬────┬────┐
│  1 │  2 │  3 │
├────┼────┼────┤
│  4 │  5 │  6 │
└────┴────┴────┘

C2:
┌────┬────┬────┐
│ 11 │ 12 │ 13 │
├────┼────┼────┤
│ 14 │ 15 │ 16 │
└────┴────┴────┘

C3:
┌────┬────┬────┐
│ 21 │ 22 │ 23 │
├────┼────┼────┤
│ 24 │ 25 │ 26 │
└────┴────┴────┘

C4:
┌────┬────┬────┐
│ 31 │ 32 │ 33 │
├────┼────┼────┤
│ 34 │ 35 │ 36 │
└────┴────┴────┘
Nếu nhìn theo channel

Bạn thấy:

C1 = [1,2,3,4,5,6]

C2 = [11,12,13,14,15,16]

C3 = [21,22,23,24,25,26]

C4 = [31,32,33,34,35,36]

Đúng hoàn toàn.

Nhưng CRNN nhìn theo width

Ta cố định:

W = 1

Lúc này lấy:

H = 1 → [1, 11, 21, 31]
H = 2 → [4, 14, 24, 34]

Gộp lại:

x1 = [1, 11, 21, 31,
      4, 14, 24, 34]

Đây là timestep 1.

Tiếp:

W = 2

ta lấy:

H = 1 → [2, 12, 22, 32]
H = 2 → [5, 15, 25, 35]

thành:

x2 = [2, 12, 22, 32,
      5, 15, 25, 35]

Cuối cùng:

W = 3

thành:

x3 = [3, 13, 23, 33,
      6, 16, 26, 36]

Vậy sequence:

x1 → x2 → x3

với:

x1 = [1,11,21,31,4,14,24,34]
x2 = [2,12,22,32,5,15,25,35]
x3 = [3,13,23,33,6,16,26,36]
Và nhìn kỹ nhé: channel 1 không bị mất

Channel 1 ban đầu:

1  2  3
4  5  6

Sau khi sequence hóa:

x1 → 1,4
x2 → 2,5
x3 → 3,6

Tức là:

C1:

1 ─────────→ x1
2 ─────────→ x2
3 ─────────→ x3
4 ─────────→ x1
5 ─────────→ x2
6 ─────────→ x3

Toàn bộ thông tin channel 1 vẫn còn nguyên.

Nó chỉ được phân bố vào các timestep khác nhau theo chiều width.

Tương tự:

C2:

11,14 → x1
12,15 → x2
13,16 → x3

C3:

21,24 → x1
22,25 → x2
23,26 → x3

C4:

31,34 → x1
32,35 → x2
33,36 → x3
Đây chính là "convert feature map → sequence"

Không phải:

Channel 1 → vector
Channel 2 → vector
...

Mà là:

                 Width
                  ↓
       W1          W2          W3
       │           │           │
       ▼           ▼           ▼
      x1          x2          x3

      x1          x2          x3
       │           │           │
       └───────────┼───────────┘
                   ↓
                  RNN

Mỗi x chứa:

toàn bộ Height
×
toàn bộ Channels
Và đây là lý do Width được chọn làm sequence

Bạn có thể hình dung ảnh chữ:

                WIDTH →
       ┌─────────────────────┐
       │    H E L L O        │
       │                     │
HEIGHT │                     │
       ↓                     │
       └─────────────────────┘

Mỗi timestep:

x1 = vùng bên trái
x2 = vùng kế tiếp
x3 = vùng kế tiếp
...
xW = vùng bên phải

RNN nhận:

x1 → x2 → x3 → ... → xW

Nó đang đọc ảnh từ trái sang phải.

Một insight rất quan trọng

Bạn vừa phân biệt được hai thứ:

Channel
C1 = một feature detector trải trên toàn bộ spatial map
Timestep
x1 = toàn bộ channels tại một spatial region theo width

Đây là hai chiều khác nhau của tensor.

Với:

H × W × C

CRNN sequence hóa theo kiểu:

W → sequence length

H × C → feature dimension

nên:

H × W × C
      ↓
W × (H × C)

Ví dụ:

14 × 28 × 512
      ↓
28 × (14 × 512)
      ↓
28 × 7168

Không có channel nào bị cắt bỏ cả. Chỉ là ta đổi cách tổ chức tensor để W trở thành chiều thời gian cho RNN.

Và nếu bạn muốn đào sâu hơn nữa, câu hỏi tiếp theo rất đáng hỏi là: "Tại sao RNN lại cần cả H × C thành feature vector? Tại sao không chỉ lấy một hàng hoặc pooling height xuống 1?" — chính câu này sẽ dẫn bạn tới cách CNN trong CRNN được thiết kế để cuối cùng có H=1, và lúc đó kiến trúc trở nên cực kỳ dễ hiểu.

đây mới là chỗ tôi cần hỏi. crnn nhìn theo width tức timestep 1 là có lấy [1][1], [2][1], v.v, tại [1][1] là 1 tensor 512, thì mỗi một giá trị của tensor này sẽ tương ứng với 1 giá trị trong channel, ví dụ tensor[0] = c1[0], tensor[1] = c2[0], .... ví dụ height = 10, nếu chỉ xet nguyên cột 1 thì cùng lắm sau đó mỗi chanel có lấy được 10 giá trị nhảy cóc, nhưng cái tôi cần hỏi 1 channel có tận 512 giá trị thì mới mạng ý nghĩa, nếu mỗi cột chỉ lấy 10 phần tử trong mỗi channel thì chẳng phải thông tin bị đứt đoạn không có ý nghĩa gì à. vì rnn sau đó là nó xử lý dữ liệu tuần tự ví dụ quét width = 1 (trong này có 10 phần tử trong mỗi channel") xử lý tạo ra h1 -> ... cảm giác bị xử lý từng khúc, mà cũng không phải từng khúc vì nó bị nhảy cóc 

À, bây giờ mình hiểu chính xác câu hỏi của bạn. Và câu hỏi này rất hay, vì bạn đang đụng vào một điểm mà nếu không phân biệt rõ thì CRNN rất dễ trở nên "vô lý".

Bạn đang nói:

Nếu Feature Map = H × W × C, ví dụ 10 × 100 × 512, thì khi lấy width=1, mình lấy 10 giá trị từ mỗi channel. Nhưng một channel có 10×100 = 1000 giá trị. Vậy mình chỉ lấy 10 giá trị rồi nhảy sang channel khác / width khác. RNN xử lý như vậy chẳng phải làm đứt đoạn thông tin spatial của channel sao?

Câu trả lời là: ĐÚNG, nếu ta hiểu feature map như một "chuỗi của từng channel". Nhưng CRNN không có mục tiêu bảo toàn mỗi channel như một sequence riêng.

Và đây chính là insight quan trọng.

1. Trước hết sửa một điểm nhỏ

Giả sử:

Feature Map = 10 × 100 × 512

Tại một cell:

[height=1, width=1]

ta có:

[
 c1(1,1),
 c2(1,1),
 c3(1,1),
 ...
 c512(1,1)
]

Đúng.

Nhưng:

c1(1,1) không phải là "phần tử thứ 1 của channel 1" theo nghĩa channel 1 là một vector dài 512.

Mà channel 1 là:

C1 = 10 × 100

tức:

C1:

        W
       1  2  3  ... 100
H=1    a  b  c  ... 
H=2    d  e  f  ...
...
H=10

c1(1,1) chỉ là một spatial activation của channel 1.

2. Và đúng: width=1 chỉ lấy 10/1000 giá trị của channel 1

Chính xác.

Nếu:

C1 = 10 × 100

thì timestep 1:

W=1

lấy:

C1:

a
d
g
...

10 giá trị.

Timestep 2:

W=2

lấy:

b
e
h
...

10 giá trị.

...

Timestep 100:

W=100

lấy:

...

10 giá trị.

Nên toàn bộ channel 1 vẫn được lấy đủ:

10 × 100 = 1000 values

Nó chỉ được phân bố:

timestep 1 → 10 values
timestep 2 → 10 values
...
timestep 100 → 10 values

Không mất dữ liệu.

3. Nhưng bạn đang hỏi sâu hơn: "Nó bị nhảy cóc!"

Đúng.

Ví dụ channel 1:

a b c d e
f g h i j
k l m n o

Nếu sequence hóa theo width:

t1 = [a, f, k]
t2 = [b, g, l]
t3 = [c, h, m]
t4 = [d, i, n]
t5 = [e, j, o]

Bạn nhìn vào channel 1 sẽ thấy:

a → f → k

rồi:

b → g → l

Nó không phải:

a → b → c → d → e

Đúng!

Và nếu RNN chỉ nhìn channel 1, thì cách này rõ ràng không giống một sequence liên tục.

4. Nhưng RNN KHÔNG nhìn channel 1

Đây là chỗ quan trọng nhất.

RNN không nhận:

channel 1 → RNN
channel 2 → RNN
...

Nó nhận toàn bộ feature vector tại mỗi width.

Ví dụ:

t1 =
[
 C1(a),
 C2(...),
 C3(...),
 ...
 C512(...)
]

cộng với toàn bộ height:

t1 =
[
 C1(H1,W1), C2(H1,W1), ..., C512(H1,W1),
 C1(H2,W1), C2(H2,W1), ..., C512(H2,W1),
 ...
 C1(H10,W1), ..., C512(H10,W1)
]

Nên:

t1 = 10 × 512 = 5120 numbers

RNN nhìn:

t1 → t2 → t3 → ... → t100

chứ không nhìn:

C1: a → f → k
5. Vậy "nhảy cóc" có vấn đề không?

Không, bởi vì sequence mà RNN cần học không phải là sequence của từng channel.

Sequence mà chúng ta muốn tạo là:

LEFT → RIGHT

của visual representation.

Hãy tưởng tượng:

ẢNH

H E L L O
↑ ↑ ↑ ↑ ↑

Ta muốn:

t1 = vùng bên trái
t2 = vùng tiếp theo
t3 = vùng tiếp theo
...

Chứ ta không quan tâm:

channel 1:
pixel 1 → pixel 2 → pixel 3

Channel chỉ là các feature detector, không phải một sequence cần RNN đọc.

6. Ví dụ cực kỳ trực quan

Giả sử CNN có 3 channels:

C1 = vertical edges
C2 = horizontal edges
C3 = curves

Đây chỉ là ví dụ trực giác, không phải CNN thực tế đảm bảo channel nào mang đúng semantic này.

Tại vùng W=1:

       H
       ↓
C1:  [edge information]
C2:  [horizontal information]
C3:  [curve information]

Ta gom thành:

t1 = [edge, horizontal, curve, ...]

Tại W=2:

t2 = [edge, horizontal, curve, ...]

...

RNN nhìn:

t1 → t2 → t3 → t4

Nó đang hỏi:

"Các visual features ở vùng bên trái liên hệ thế nào với visual features ở vùng kế bên?"

Đây chính là thứ OCR cần.

7. Nhưng bạn vẫn có một nghi vấn rất hợp lý

Bạn có thể nói:

"Nhưng height=10 cũng bị gom hết vào một timestep. Vậy spatial relationship giữa H1, H2, H3... thì sao?"

Đây chính là lý do CNN phải xử lý spatial information trước RNN.

CNN đã dùng convolution:

pixel
 ↓
local features
 ↓
higher-level features
 ↓
higher-level spatial representation

Nên khi đến RNN:

CNN output

đã là một representation chứa thông tin spatial.

RNN không phải chịu trách nhiệm thay thế CNN.

8. Và đây là lý do kiến trúc thực tế thường ép Height → 1

Đây mới là phần có thể giải quyết hoàn toàn cảm giác "bị cắt khúc" của bạn.

Thay vì:

10 × 100 × 512

nhiều CRNN thiết kế CNN để cuối cùng thành:

1 × 100 × 512

Lúc này:

width 1 → [512 values]
width 2 → [512 values]
width 3 → [512 values]
...

Sequence:

[512] → [512] → [512] → ... → [512]

Không còn chuyện lấy 10 giá trị rải theo height nữa.

Đây là representation cực kỳ tự nhiên cho RNN.

9. Vậy CNN làm thế nào để Height giảm xuống 1?

Ví dụ:

224 × 224
   ↓
112 × 112
   ↓
56 × 56
   ↓
28 × 28
   ↓
14 × 28
   ↓
1 × 28

CNN/pooling/stride được thiết kế để:

HEIGHT ↓↓↓↓↓
WIDTH  ↓↓↓

nhưng thường giữ tương đối nhiều thông tin theo WIDTH, vì WIDTH chính là chiều ta muốn biến thành sequence.

Cuối cùng:

1 × W × C

rất đẹp cho OCR.

10. Khi đó hãy nhìn lại ví dụ của bạn

Ban đầu:

10 × 100 × 512

bạn lo:

channel 1:

a b c d e ...
f g h i j ...
...

↓ sequence

t1 = a,f,k,...
t2 = b,g,l,...

và cảm giác:

"Nó bị nhảy cóc!"

Đúng.

Nhưng kiến trúc tốt thường làm:

10 × 100 × 512
       ↓ CNN
1 × 100 × 512

bây giờ:

channel 1:

a b c d e ... 

và sequence:

t1 = [C1(a), C2(a), ..., C512(a)]

t2 = [C1(b), C2(b), ..., C512(b)]

t3 = [C1(c), C2(c), ..., C512(c)]

Đây mới là thứ bạn đang tưởng tượng ban đầu.

11. Có một insight còn sâu hơn nữa

Thực ra:

"Channel" không phải thứ RNN cần bảo toàn theo chiều sequence.

CNN tạo ra một representation space:

spatial location × feature channels

Ví dụ:

          Width →
       x1    x2    x3    x4
      ┌────┬────┬────┬────┐
H1    │512 │512 │512 │512 │
H2    │512 │512 │512 │512 │
H3    │512 │512 │512 │512 │
      └────┴────┴────┴────┘

RNN muốn:

x1 → x2 → x3 → x4

Mỗi x là một representation của một vùng không gian.

Channel chỉ là các chiều của representation đó.

Giống như NLP:

"I" → [0.2, 0.8, -0.1, ...]

Bạn không hỏi:

"Tại sao dimension 1 của embedding bị tách khỏi dimension 2?"

Bởi vì:

[0.2, 0.8, -0.1, ...]

là một vector representation.

CNN feature vector cũng tương tự.

12. Có thể hình dung CRNN như thế này
                 CNN
                  │
                  ▼

      visual representation
                  
     x1       x2       x3       x4
   [512]    [512]    [512]    [512]
      │        │        │        │
      └────────┴────────┴────────┘
                       │
                      RNN
                       │
                       ▼
                  sequence
                       │
                       ▼
                    "HELLO"

CNN nói:

"Tại vị trí x1, tôi thấy những visual features này."

"Tại vị trí x2, tôi thấy những visual features này."

RNN nói:

"À, x1 rồi x2 rồi x3 liên tiếp với nhau tạo thành pattern gì?"

Và mình nghĩ câu hỏi của bạn thực ra đã chạm đến một điều rất quan trọng

Bạn đang phân biệt:

"channel là một sequence"

với:

"channel là một dimension của feature vector"

Trong CRNN, cái thứ hai mới đúng.

Nếu output CNN là:

1 × W × C

thì:

W = sequence length
C = feature dimension

Ví dụ:

1 × 100 × 512

→ RNN nhận:

100 timesteps
×
512-dimensional feature vector

tức:

x1 [512]
x2 [512]
x3 [512]
...
x100 [512]

Không phải 512 sequence, mỗi sequence dài 100.

Và nếu bạn muốn hiểu thật chắc phần này, bước tiếp theo rất đáng làm là lấy đúng tensor 2 × 3 × 4, rồi mình cho bạn xem cùng một tensor đó dưới 3 góc nhìn: channel-wise, pixel-wise và sequence-wise. Khi thấy 3 cách indexing của cùng một tensor, cái "nhảy cóc" bạn đang lo sẽ trở nên rất rõ.

hiểu đoạn này rồi nhưng tôi lại chưa hiểu đoạn chuyển từ vector -> text, ví dụ qua cnn -> ... -> RNN -> sẽ cho ra h1 = vector -> linear -> 1 số duy nhất, rồi sao nữa

Đúng, đây là mảnh ghép cuối để hiểu CRNN + CTC. Và có một chỗ cần sửa:

Linear không cho ra 1 số duy nhất. Nó cho ra một vector score/probability có kích thước bằng số class.

Ví dụ ta có alphabet:

A B C ... Z blank

→ 27 classes.

1. RNN cho ra h1, h2, ... chứ không phải text

Giả sử CNN tạo sequence:

x1 → x2 → x3 → ... → x20

BiLSTM xử lý:

x1 → h1
x2 → h2
x3 → h3
...
x20 → h20

Mỗi h là một vector, ví dụ:

h1 = [0.2, 0.7, -0.3, ..., 0.8]

Giả sử hidden size = 256:

h1.shape = [256]
2. Linear không biến h1 thành một số

Giả sử OCR chỉ nhận:

A B C ... Z blank

27 class.

Ta có:

Linear(256 → 27)

Nó nhận:

h1 = [256 numbers]

và tạo:

y1 = [27 numbers]

Ví dụ:

y1 =
[
  0.1,   # A
  0.2,   # B
  0.05,  # C
  ...
  8.7,   # H
  ...
  0.3    # blank
]

Sau softmax:

P(y1) =
[
  0.001, # A
  0.002, # B
  0.0005,# C
  ...
  0.91,  # H
  ...
  0.001 # blank
]

→ model nói:

timestep 1 → khả năng cao là H
3. Và quan trọng: không chỉ có h1

Ta có toàn bộ:

h1
h2
h3
...
h20

Linear được áp dụng cho từng timestep:

h1  → Linear → y1 = 27 scores
h2  → Linear → y2 = 27 scores
h3  → Linear → y3 = 27 scores
...
h20 → Linear → y20 = 27 scores

Vậy output cuối cùng là:

20 × 27

Nó có thể hình dung:

             A    B    C   ... H ... Z blank
t1          .1   .2   .1  ... 8.7 ... .1  .3
t2          .2   .1   .0  ... 7.9 ... .2  .2
t3          .1   .1   .2  ... 6.2 ... .1  5.8
t4          .1   .1   .1  ... .2  ... .2  9.1
t5          .1   .1   .1  ... .3  ... .1  8.9
...
4. Lấy class có score cao nhất thì sao?

Nếu ta đơn giản argmax:

t1 → H
t2 → H
t3 → blank
t4 → E
t5 → E
t6 → blank
t7 → L
t8 → L
t9 → L
t10 → blank
t11 → L
t12 → O
t13 → O

Ta được:

H H blank E E blank L L L blank L O O

Đây vẫn chưa phải "HELLO".

Đây chính là chỗ CTC xuất hiện.

5. CTC làm gì?

CTC có một quy tắc đơn giản khi decode:

Bước 1: bỏ các ký tự lặp liên tiếp
H H → H
E E → E
L L L → L
O O → O
Bước 2: bỏ blank
H H blank E E blank L L L blank L O O

↓

H E L L O

↓

HELLO
6. Nhưng tại sao phải có blank?

Đây là một ý tưởng cực kỳ hay.

Giả sử muốn nhận dạng:

LL

Nếu không có blank, model có thể output:

L L

Nhưng CTC cần phân biệt:

L

với:

LL

Ví dụ:

L blank L

→ LL

Trong khi:

L L

→ sau collapse thành L.

Cho nên:

L L

đại diện cho một L kéo dài

còn:

L blank L

đại diện cho hai L riêng biệt.

7. Đây là toàn bộ CRNN

Bây giờ nối lại:

IMAGE
  │
  ▼
CNN
  │
  ▼
Feature Map
  │
  ▼
Sequence
  │
  ▼
x1 x2 x3 ... x20
  │  │  │       │
  ▼  ▼  ▼       ▼
BiLSTM
  │  │  │       │
  ▼  ▼  ▼       ▼
h1 h2 h3 ... h20
  │  │  │       │
  ▼  ▼  ▼       ▼
Linear
  │  │  │       │
  ▼  ▼  ▼       ▼
y1 y2 y3 ... y20
 │  │  │       │
 ▼  ▼  ▼       ▼
27 classes mỗi timestep
  │
  ▼
argmax
  │
  ▼
H H blank E E blank L L L blank L O O
  │
  ▼
CTC decode
  │
  ▼
HELLO
8. Nhưng có một thứ rất quan trọng: trong lúc TRAIN thì không đơn giản như vậy

Khi inference:

probabilities
    ↓
decode
    ↓
HELLO

thì bạn có thể hiểu đơn giản như trên.

Nhưng khi training, ta có:

Image → CNN → RNN → Linear
                       ↓
                probabilities
                       ↓
                    CTC Loss
                       ↑
                    "HELLO"

Ta đưa label thật:

HELLO

cho CTC Loss.

CTC tìm xem có những alignment nào có thể biến thành HELLO.

Ví dụ:

H H blank E E blank L L L blank L O O

là một alignment hợp lệ.

Nhưng cũng có thể:

blank H H E blank E L L blank L O O blank

v.v.

Có rất nhiều cách căn chỉnh sequence dài 20 timestep với label dài 5 ký tự.

CTC tính tổng xác suất của các alignment hợp lệ đó.

9. Đây là điểm cực kỳ hay của CTC

Ảnh có:

HELLO

nhưng bạn không cần nói cho model biết:

timestep 1-3 = H
timestep 4-6 = E
timestep 7-10 = L
...

Bạn chỉ cần:

input:
[image]

target:
"HELLO"

CTC tự xử lý alignment.

10. Và đây là lý do output không phải "một số"

Bạn vừa hỏi:

h1 = vector -> linear -> 1 số duy nhất, rồi sao nữa

Thực tế:

h1 = vector 256 chiều

      ↓ Linear

y1 = vector 27 chiều

      ↓ Softmax

P(A), P(B), ..., P(Z), P(blank)

      ↓ argmax

một class

Ví dụ:

h1
 ↓
Linear
 ↓
[0.1, 0.2, ..., 8.7, ..., 0.3]
 ↓
Softmax
 ↓
[0.01, 0.02, ..., 0.91, ..., 0.01]
                         ↑
                         H

Chỉ sau khi lấy argmax mới ra một class duy nhất cho timestep đó.

Và vì có nhiều timestep:

t1 → H
t2 → H
t3 → blank
t4 → E
...

nên cuối cùng mới có một chuỗi ký tự.

Có thể nhớ bằng 3 tầng
h1 = "representation"
       ↓
Linear = "classification"
       ↓
class probabilities
       ↓
CTC = "sequence decoding"
       ↓
text

Hay cụ thể:

vector
  ↓
Linear
  ↓
"các khả năng A-Z + blank"
  ↓
nhiều timestep
  ↓
CTC
  ↓
HELLO

Và đây cũng là lý do CRNN không phải Seq2Seq theo nghĩa encoder-decoder truyền thống. CRNN+CTC thường giữ chiều dài timestep của CNN/RNN và dự đoán class tại từng timestep, rồi CTC xử lý alignment; còn Seq2Seq kiểu encoder-decoder thì decoder sinh token từng bước dựa trên các token trước đó. Đây là một khác biệt rất đáng hiểu nếu bạn đang học sâu RNN/Seq2Seq.

linear y = Wx + b á hay mạng nơ ron, hay softmax, linear dự đoán 1 số chứ có tạo mảng đâu

Đúng, chỗ này cần phân biệt một neuron Linear với một layer Linear. Bạn đang nghĩ đúng ở mức neuron.

1. Một neuron → đúng là 1 số

Công thức:

$$ y = Wx + b $$

Nếu:

x = [x1, x2, x3, x4]   # 4 số
W = [w1, w2, w3, w4]
b = số

thì:

$$ y = w_1x_1+w_2x_2+w_3x_3+w_4x_4+b $$

Kết quả:

y = 7.23

Một neuron → một số.

2. Nhưng Linear(256, 27) là 27 neuron

Đây mới là chỗ quan trọng.

Khi ta viết:

nn.Linear(256, 27)

thì không phải một neuron.

Nó là 27 neuron song song:

                 ┌── neuron 1 ──> y1
h (256 số) ──────┼── neuron 2 ──> y2
                 ├── neuron 3 ──> y3
                 │      ...
                 └── neuron 27 ─> y27

Mỗi neuron có:

256 weights + 1 bias

nên toàn layer có:

$$ W: 27\times256 $$

và:

$$ b: 27 $$

Tính:

$$ y = Wx+b $$

thì:

x: [256]
W: [27, 256]
b: [27]

y: [27]

Tức là Linear tạo ra một vector 27 số, bởi vì nó chứa 27 neuron.

3. Trong OCR thì 27 số này là gì?

Ví dụ ta có:

h1 = [256 numbers]

Đưa qua:

Linear(256, 27)

ta nhận:

y1 = [
    2.1,   # score cho A
    -0.3,  # score cho B
    1.7,   # score cho C
    ...
    8.2    # score cho blank
]

Sau Softmax:

[
  0.02,   # P(A)
  0.001,  # P(B)
  0.01,   # P(C)
  ...
  0.91    # P(blank)
]

Nên Softmax cũng không tự tạo ra mảng.

Nó nhận mảng 27 số từ layer Linear rồi biến thành mảng 27 xác suất.

4. Và đây chính là lý do OCR có T × 27

Giả sử CNN + RNN tạo ra:

h1
h2
h3
...
h20

Mỗi h có 256 số:

20 × 256

Cho từng h qua cùng một Linear(256, 27):

h1  ──> Linear ──> [27]
h2  ──> Linear ──> [27]
h3  ──> Linear ──> [27]
...
h20 ──> Linear ──> [27]

Kết quả:

20 × 27

Có thể hình dung:

             A    B    C    ...   Z   blank
t1          0.1  0.2  0.01  ...  0.3  0.05
t2          0.8  0.01 0.02  ...  0.1  0.01
t3          0.02 0.1  0.7   ...  0.1  0.03
...
t20         ...

Sau đó mới chọn class có xác suất cao nhất ở mỗi timestep.

Tóm lại:

1 neuron
    ↓
y = Wx + b
    ↓
1 số


1 Linear layer có 27 neuron
    ↓
y = Wx + b
    ↓
27 số


20 timestep
    ↓
mỗi timestep qua Linear 27 neuron
    ↓
20 × 27 số
    ↓
Softmax
    ↓
20 × 27 probabilities
    ↓
CTC decode
    ↓
"HELLO"

Vậy câu “Linear dự đoán 1 số” của bạn là đúng nếu đang nói về một neuron. Trong CRNN, Linear(256, 27) là 27 neuron, nên nó tạo ra 27 số, mỗi số tương ứng với một class ký tự.