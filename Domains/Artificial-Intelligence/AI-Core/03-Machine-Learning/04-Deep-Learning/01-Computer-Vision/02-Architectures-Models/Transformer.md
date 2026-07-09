Đây là một chủ đề rất lớn. Nếu học đầy đủ từ đầu đến production thì Transformer trong Computer Vision (CV) có thể là cả một khóa học.

Mình sẽ giải thích theo cách mà các kỹ sư AI ở Google, OpenAI hay Meta thường hiểu, bắt đầu từ trực giác rồi mới đi đến kiến trúc.

Lộ trình
1. CNN có vấn đề gì?

↓

2. Tại sao Transformer lại được mang sang CV?

↓

3. Ý tưởng cốt lõi

↓

4. Ảnh được biến thành Token như thế nào?

↓

5. Positional Embedding

↓

6. Self-Attention trên ảnh

↓

7. Multi-Head Attention

↓

8. Encoder

↓

9. Vision Transformer (ViT)

↓

10. Swin Transformer

↓

11. DETR

↓

12. Segment Anything (SAM)

↓

13. DINOv2

↓

14. Production Pipeline
Chương 1
Trước Transformer

Trong hơn 20 năm.

Computer Vision gần như là

Image

↓

CNN

↓

Prediction

Ví dụ

Image

↓

ResNet

↓

Cat

Hoặc

Image

↓

YOLO

↓

Bounding Box

CNN rất mạnh.

Nhưng có một vấn đề.

Giả sử ảnh.

🐱                         🐶

Con mèo.

Ở góc trái.

Con chó.

Ở góc phải.

CNN ban đầu chỉ nhìn.

3x3

Sau đó

5x5

Sau đó

7x7

Nó mở rộng dần.

Tức là.

CNN học.

Local Information

Trước.

Rồi mới.

Global Information

Nếu muốn thấy toàn bộ ảnh.

CNN cần.

30

40

50

100

Layer

Đây là nhược điểm.

Transformer

Transformer nghĩ khác.

Ngay layer đầu tiên.

Nó đã nhìn.

Toàn bộ ảnh.

Đó là điểm khác biệt lớn nhất.

NLP

Trong NLP.

Transformer nhận.

I

love

cats

↓

Token.

Self Attention.

love

↓

cats

Có liên quan.

CV

Transformer nhận.

Image

↓

Patch.

Self Attention.

Patch A

↓

Patch B

Có liên quan.

Đây là ý tưởng giống hệt.

Khác duy nhất.

Token không còn là từ nữa.

Mà là.

Patch.
Chương 2

Ảnh biến thành Token thế nào?

Giả sử ảnh.

224 × 224

Ta chia.

16 × 16

patch.

Ta được.

□ □ □ □

□ □ □ □

□ □ □ □

□ □ □ □

Thực tế.

14 × 14

=

196 patch

Mỗi patch.

16 × 16 × 3

Được flatten.

768 numbers

Ví dụ.

Patch

↓

[0.1,

0.4,

0.2,

...]

768 values

Đây gọi là.

Patch Embedding.

Giờ.

Transformer nghĩ.

Patch

=

Word
So sánh NLP và CV
NLP	CV
Sentence	Image
Word	Patch
Token Embedding	Patch Embedding
Position Embedding	Position Embedding
Self Attention	Self Attention
Encoder	Encoder

Kiến trúc gần như giống nhau.

Positional Embedding

Nếu chỉ đưa patch.

Transformer sẽ không biết.

Patch này ở đâu.

Ví dụ.

□ □ □ □

Không biết.

Đây là.

Top Left

Hay.

Bottom Right

Nên.

ViT thêm.

Patch Embedding

+

Position Embedding

Ví dụ.

Patch 1

+

Position 1

↓

Input.

Self Attention

Đây là trái tim.

Giả sử.

Patch.

Mặt mèo

Patch.

Tai mèo

Patch.

Mắt mèo

Self Attention.

Biết.

Tai

↓

Mắt

↓

Mũi

↓

Lông

Có liên quan.

CNN.

Chỉ thấy.

3x3

Transformer.

Nhìn.

Toàn bộ 196 patch.

Ngay lập tức.

Multi Head Attention

Không chỉ có.

1 attention.

Mà.

Head 1

↓

Texture

Head 2.

Shape

Head 3.

Color

Head 4.

Object Relation

Các Head học.

Những thứ khác nhau.

Vision Transformer

Pipeline.

Image

↓

Split Patch

↓

Patch Embedding

↓

Position Embedding

↓

Transformer Encoder ×12

↓

MLP Head

↓

Prediction

Ví dụ.

Cat

98%
DETR

Đây là.

Transformer cho.

Object Detection.

Ngày xưa.

YOLO.

CNN

↓

Anchor

↓

NMS

DETR.

Image

↓

Transformer

↓

Object Queries

↓

Bounding Box

Không cần.

Anchor.

Swin Transformer

ViT.

Có vấn đề.

Attention.

196 patch

↓

196².

Ảnh.

1024×1024.

↓

Attention.

Rất lớn.

Swin.

Chỉ attention.

Trong.

Window.

Ví dụ.

□ □

□ □

Sau đó.

Window.

Dịch đi.

↓

Shifted Window.

Kết quả.

Nhanh hơn.

Ít RAM hơn.

Segment Anything (SAM)

Meta.

Dùng.

Vision Transformer.

Pipeline.

Image

↓

Image Encoder

(ViT)

↓

Prompt Encoder

↓

Mask Decoder

↓

Segmentation

Ví dụ.

Bạn click.

Con mèo

SAM.

↓

Tách.

Con mèo.

DINOv2

Meta.

Không cần Label.

Image.

↓

Vision Transformer.

↓

Embedding.

Embedding.

Có thể dùng.

Search

Classification

Detection

Clustering
Có giống NLP không?

Câu trả lời.

90% giống.

Khác.

Đầu vào.

NLP.

Sentence

↓

Token

CV.

Image

↓

Patch

Sau đó.

Embedding

↓

Position

↓

Transformer Encoder

↓

Attention

Hoàn toàn giống.

Transformer trong CV có thay thế CNN không?

Không hoàn toàn.

Hiện nay.

Production.

Rất nhiều mô hình.

CNN

+

Transformer

Ví dụ.

ConvNeXt
EfficientFormer
MobileViT
CoAtNet

Đều.

Hybrid.

Production

Ví dụ.

ChatGPT Vision.

Image

↓

Vision Transformer

↓

Image Embedding

↓

LLM

↓

Answer

Gemini.

Image

↓

Vision Encoder

↓

Transformer

↓

LLM

SAM.

Image

↓

Vision Transformer

↓

Segmentation

CLIP.

Image

↓

Vision Transformer

Song song.

Text

↓

Transformer

↓

Hai embedding được đưa vào cùng một không gian vector để mô hình học rằng ảnh "mèo" và câu "a cat" nên ở gần nhau.

Kiến thức nền nên học theo thứ tự

Nếu mục tiêu của bạn là hiểu Transformer trong CV đến mức có thể đọc paper và xây hệ thống production, lộ trình hợp lý là:

CNN cơ bản: Convolution, Pooling, Feature Map, Receptive Field.
Transformer trong NLP: Attention, Multi-Head Attention, Positional Encoding, Encoder.
Vision Transformer (ViT): Patch Embedding, Class Token, ViT Encoder.
Các biến thể: Swin Transformer, DETR, CLIP, DINOv2, SAM.
Ứng dụng thực tế: Classification, Detection, Segmentation, Retrieval, Vision-Language Models (VLM).
Tóm tắt dễ nhớ

Bạn có thể ghi nhớ bằng bảng sau:

NLP Transformer	Vision Transformer
Câu văn	Ảnh
Word	Image Patch
Token Embedding	Patch Embedding
Positional Embedding	Positional Embedding
Self-Attention giữa các từ	Self-Attention giữa các patch
Encoder	Encoder
Dự đoán từ tiếp theo hoặc phân loại	Phân loại ảnh, phát hiện vật thể, phân đoạn, tạo embedding

Điểm khác biệt lớn nhất chỉ nằm ở cách biểu diễn đầu vào:

NLP: biến câu thành chuỗi token.
CV: chia ảnh thành các patch rồi coi mỗi patch như một token.

Sau bước đó, phần lớn kiến trúc Transformer (Embedding → Positional Encoding → Multi-Head Self-Attention → Feed Forward → LayerNorm → Encoder Stack) hoạt động theo cùng một nguyên lý. Chính vì vậy, khi bạn đã hiểu Transformer trong NLP, việc học Vision Transformer sẽ nhanh hơn rất nhiều.