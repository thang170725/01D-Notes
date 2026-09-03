LeNet

LeNet-5 là một trong những CNN kinh điển, do Yann LeCun và cộng sự phát triển cho nhận dạng chữ số viết tay.

Image
 ↓
Conv
 ↓
Pooling
 ↓
Conv
 ↓
Pooling
 ↓
FC
 ↓
Class
Dùng để làm gì?

Classification đơn giản:

7 → class 7
3 → class 3
Khi nào dùng?

Ngày nay gần như không dùng LeNet cho production, nhưng cực kỳ đáng học để hiểu:

convolution
pooling
feature map
FC
CNN classification

LeNet = CNN nhập môn.

2. AlexNet

AlexNet nổi tiếng từ ImageNet 2012 và là một cột mốc quan trọng khiến Deep Learning/CNN bùng nổ trong Computer Vision.

Ý tưởng lớn:

Image
 ↓
Deep CNN
 ↓
Feature extraction
 ↓
Classification

Điểm quan trọng trong lịch sử:

CNN sâu hơn
GPU training
ReLU
dropout
data augmentation
ImageNet-scale training
Khi nào dùng?

Ngày nay thường không chọn AlexNet cho model mới, nhưng học nó để hiểu:

Tại sao CNN từ những network nhỏ bắt đầu trở thành deep CNN?

3. EfficientNet

EfficientNet tập trung vào câu hỏi:

Làm sao tăng accuracy mà không tăng computation quá lãng phí?

Thay vì chỉ:

depth ↑

EfficientNet dùng ý tưởng compound scaling:

Depth       ↑
Width       ↑
Resolution  ↑

theo tỷ lệ được cân bằng.

Có:

EfficientNet-B0
EfficientNet-B1
...
EfficientNet-B7
Dùng khi nào?

Khi bạn cần:

classification
backbone
accuracy tốt / computation hợp lý
model tương đối nhẹ

Ví dụ edge/mobile deployment.

EfficientNet = chú trọng hiệu quả.

4. ConvNeXt

ConvNeXt là một CNN hiện đại được thiết kế bằng cách:

lấy nhiều ý tưởng từ Vision Transformer rồi áp dụng lại cho CNN.

Nó cho thấy CNN vẫn rất mạnh nếu thiết kế hiện đại.

CNN
 ↑
Transformer-inspired design
Khi nào dùng?
image classification
backbone cho detection
segmentation
visual feature extraction

Nếu bạn muốn hiểu:

CNN hiện đại cạnh tranh với ViT như thế nào?

thì ConvNeXt rất đáng học.

Detection

Detection trả lời:

Object là gì + nằm ở đâu?

Ví dụ:

Image
 ↓
┌──────────────┐
│     CAT      │
└──────────────┘

Output:

class = cat
bbox = (x1, y1, x2, y2)
confidence = 0.95
5. SSD

SSD = Single Shot MultiBox Detector.

Ý tưởng:

Detect object trong một forward pass.

Image
 ↓
CNN
 ↓
Multiple feature maps
 ↓
Boxes + Classes

SSD sử dụng nhiều feature maps ở các scale khác nhau để detect object lớn/nhỏ.

Dùng khi nào?
real-time object detection
edge devices
cần model tương đối đơn giản

SSD = detection nhanh, kiến trúc tương đối trực tiếp.

6. RetinaNet

RetinaNet giải quyết một vấn đề lớn của one-stage detector:

Foreground quá ít so với background.

Ví dụ:

10000 candidate locations

Object:
████ 10

Background:
░░░░ 9990

Model dễ bị background áp đảo.

RetinaNet đưa ra Focal Loss:

easy negative
     ↓
giảm trọng số

hard example
     ↓
tập trung học
Khi nào dùng?

Khi muốn hiểu:

one-stage detector
class imbalance
Focal Loss

RetinaNet = one-stage detection + giải quyết class imbalance.

7. DETR

DETR = DEtection TRansformer.

Đây là bước chuyển rất quan trọng:

CNN-based detection
        ↓
Transformer-based detection

DETR coi object detection gần với một set prediction problem.

Kiến trúc ý tưởng:

Image
 ↓
CNN backbone
 ↓
Transformer Encoder
 ↓
Transformer Decoder
 ↓
Object Queries
 ↓
Objects
Dùng khi nào?
modern object detection
nghiên cứu Transformer vision
muốn hiểu object queries
end-to-end detection

DETR là một trong những model quan trọng nhất để hiểu Transformer bước vào Computer Vision.

Segmentation

Detection:

"Object ở đâu?"
→ bounding box

Segmentation:

"Pixel nào thuộc object?"

Ví dụ:

background background
background person
background person
8. FCN

FCN = Fully Convolutional Network.

Ý tưởng quan trọng:

Biến CNN classification thành network có thể output pixel-level prediction.

Image
 ↓
CNN
 ↓
Feature map
 ↓
Upsampling
 ↓
Pixel classes
Dùng:

Semantic segmentation.

Ví dụ:

pixel → road
pixel → car
pixel → sky

FCN = nền móng của deep-learning semantic segmentation.

9. U-Net

U-Net cực kỳ nổi tiếng trong segmentation.

Kiến trúc:

        Encoder
       /        \
Image →          → Output mask
       \        /
        Decoder

Điểm đặc biệt:

skip connections.

Encoder feature
      │
      └──────────────→ Decoder

Encoder hiểu:

object là gì?

Decoder cần:

object nằm chính xác ở pixel nào?

Skip connection giúp giữ spatial information.

Khi nào dùng?
medical imaging
document segmentation
binary segmentation
semantic segmentation
ít dữ liệu training

U-Net = segmentation model kinh điển và cực kỳ đáng học.

10. DeepLab

DeepLab tập trung vào semantic segmentation với:

Dilated/Atrous convolution

Thay vì:

3×3

lấy vùng receptive field lớn hơn mà không cần giảm resolution quá nhiều.

normal convolution

● ● ●
● ● ●
● ● ●

Atrous:

● . ● . ●
. . . . .
● . ● . ●
Dùng khi:
semantic segmentation
cần context lớn
muốn giữ spatial resolution tốt

DeepLab = segmentation + atrous convolution + multi-scale context.

11. Mask R-CNN

Mask R-CNN mở rộng Faster R-CNN:

Object detection
+
Instance segmentation

Output:

Person 1
 ├── bbox
 ├── class
 └── mask

Person 2
 ├── bbox
 ├── class
 └── mask

Khác semantic segmentation:

person person

Mask R-CNN phân biệt:

person #1
person #2
Dùng khi:
instance segmentation
robotics
medical
object-level analysis
12. SegFormer

SegFormer là segmentation architecture dựa trên Transformer.

Ý tưởng:

Image
 ↓
Transformer encoder
 ↓
Multi-scale features
 ↓
Lightweight decoder
 ↓
Segmentation
Dùng:
semantic segmentation
modern Transformer-based segmentation

SegFormer = một ví dụ rất tốt để học Transformer cho segmentation.

13. SAM

SAM = Segment Anything Model.

Ý tưởng lớn:

Không chỉ segmentation một class cụ thể; model có thể segment object dựa trên prompt.

Prompt có thể là:

point
box
mask

Ví dụ:

Image
 +
point vào con mèo
 ↓
SAM
 ↓
mask con mèo
Dùng:
interactive segmentation
annotation
image editing
object extraction
segmentation foundation model

SAM = segmentation trở thành một foundation-model task.

Pose Estimation

Pose estimation trả lời:

Các keypoint của cơ thể nằm ở đâu?

Ví dụ:

      ● head
      |
   ●--●--●
      |
      ●
     / \
    ●   ●
14. OpenPose

OpenPose là một framework nổi tiếng cho human pose estimation.

Nó detect:

head
shoulder
elbow
wrist
hip
knee
ankle
...
Dùng:
human pose
action recognition
gesture
motion analysis
15. HRNet

HRNet = High-Resolution Network.

Ý tưởng:

Giữ feature resolution cao trong suốt quá trình network hoạt động.

Điều này rất hữu ích cho:

keypoint localization

vì keypoint cần chính xác vị trí.

Dùng:
pose estimation
keypoint detection
segmentation

HRNet = rất mạnh khi spatial precision quan trọng.

Tracking

Detection:

Frame 1 → person
Frame 2 → person

Tracking muốn biết:

person A ở frame 1
      ↓
person A ở frame 2
      ↓
person A ở frame 3
16. DeepSORT

DeepSORT:

Detector
   ↓
Bounding boxes
   ↓
Deep appearance feature
   +
Motion model
   ↓
Tracking IDs

Ví dụ:

Person A → ID 1
Person B → ID 2
Dùng:
multi-object tracking
surveillance
traffic
people tracking
17. ByteTrack

ByteTrack có một insight rất hay:

Đừng vứt bỏ tất cả low-confidence detections.

Một detection confidence thấp đôi khi vẫn là:

object thật

đặc biệt khi object bị che.

ByteTrack tận dụng cả:

high-score boxes
+
low-score boxes

để associate tracks.

Dùng:
real-time multi-object tracking
traffic
people tracking

ByteTrack = MOT rất đáng học nếu bạn muốn hiểu tracking hiện đại.

OCR

Đây là phần rất gần với hướng bạn đang học.

18. EAST

EAST = Efficient and Accurate Scene Text detector.

Nó giải quyết:

Text nằm ở đâu trong ảnh?

Ví dụ:

Image
 ↓
EAST
 ↓
Text boxes

Không phải:

HELLO

mà là:

┌──────────────┐
│              │
└──────────────┘
Dùng:

Scene text detection.

19. CRNN

CRNN = CNN + RNN + CTC.

Đây là model mình đặc biệt khuyên bạn học nếu đang muốn hiểu OCR.

Text image
 ↓
CNN
 ↓
Visual features
 ↓
BiLSTM
 ↓
Sequence
 ↓
CTC
 ↓
"HELLO"

CNN:

nhìn hình ảnh.

BiLSTM:

hiểu sequence.

CTC:

align sequence mà không cần character-level bounding box.

Khi nào dùng?
OCR recognition
scene text recognition
text line recognition

CRNN là cây cầu cực đẹp giữa CNN → RNN → CTC.

20. PaddleOCR

PaddleOCR không phải một architecture đơn lẻ kiểu LeNet.

Nó là OCR toolkit/ecosystem, gồm nhiều component:

Detection
 ↓
Recognition
 ↓
Post-processing

Có thể sử dụng nhiều architecture khác nhau.

Dùng:

Khi bạn muốn:

"Tôi cần OCR chạy được."

Trong khi:

CRNN

phù hợp hơn khi bạn muốn:

"Tôi muốn hiểu OCR recognition hoạt động thế nào."

Vision Transformer
21. ViT

ViT = Vision Transformer.

Thay vì CNN:

pixels
 ↓
convolution

ViT chia ảnh thành patches:

Image

┌─┬─┬─┬─┐
├─┼─┼─┼─┤
├─┼─┼─┼─┤
└─┴─┴─┴─┘

Mỗi patch → token.

Image
 ↓
Patchify
 ↓
Tokens
 ↓
Transformer
 ↓
Classification
Dùng:
classification
visual backbone
foundation vision models

ViT = điểm bắt đầu để hiểu Transformer trong vision.

22. DeiT

DeiT = Data-efficient Image Transformer.

ViT thường cần rất nhiều data.

DeiT nghiên cứu:

Làm thế nào train ViT hiệu quả hơn với ít dữ liệu hơn?

Một ý tưởng quan trọng là knowledge distillation.

Dùng:

Khi nghiên cứu:

efficient ViT training
distillation
data efficiency
23. Swin Transformer

Swin = Shifted Window Transformer.

Global self-attention của ViT rất tốn computation khi ảnh lớn.

Swin chia attention thành windows:

┌──┬──┬──┐
│  │  │  │
├──┼──┼──┤
│  │  │  │
├──┼──┼──┤
│  │  │  │
└──┴──┴──┘

Sau đó shift window.

Dùng:
classification
detection
segmentation
backbone

Swin = Transformer được thiết kế để xử lý ảnh lớn hiệu quả hơn.

24. ConvNeXt V2

ConvNeXt V2 tiếp tục phát triển ConvNeXt.

Kết hợp các ý tưởng hiện đại như:

improved ConvNet architecture
large-scale pretraining
masked autoencoder / feature learning ideas
Dùng:
vision backbone
classification
detection
segmentation
Multimodal
25. CLIP

CLIP học:

Image ↔ Text

Ví dụ:

Image encoder
     ↓
image embedding

Text encoder
     ↓
text embedding

Sau đó đưa hai embedding vào cùng một space.

cat image
   ↕
"photo of a cat"
Dùng:
zero-shot classification
image-text retrieval
image search
multimodal foundation models

Điểm rất quan trọng:

CLIP không phải OCR model.

Nó học quan hệ:

image ↔ language
26. SigLIP

SigLIP cũng học image-text alignment giống CLIP nhưng thay đổi objective/loss.

Thay vì cách contrastive softmax loss truyền thống của CLIP, SigLIP dùng sigmoid-based pairwise objective.

Dùng:
image-text retrieval
multimodal models
vision-language representation
Generative Vision

Đây là một nhánh rất lớn.

27. AutoEncoder

AutoEncoder:

Image
 ↓
Encoder
 ↓
Latent
 ↓
Decoder
 ↓
Reconstructed Image

Mục tiêu:

input ≈ output

Encoder:

nén thông tin.

Decoder:

giải nén.

Dùng:
dimensionality reduction
representation learning
reconstruction
anomaly detection
28. Sparse AutoEncoder

Thêm constraint:

latent representation nên sparse.

Ví dụ:

100 latent neurons

0 0 0 1 0 0 0 0 1 0 ...

Chỉ một số neuron active.

Dùng:
representation learning
interpretability
feature discovery
29. Denoising AutoEncoder

Input bị noise:

clean image
 ↓
add noise
 ↓
noisy image

Model học:

noisy
 ↓
AE
 ↓
clean
Dùng:
denoising
robust representation learning
30. VAE

VAE = Variational AutoEncoder.

Khác AE:

AE:
image → latent vector

VAE:
image → distribution

Encoder học:

μ
σ

Sau đó sample:

z = μ + σ ε
Dùng:
generative modeling
latent representation
image generation
31. ELBO

ELBO là objective quan trọng trong VAE.

Nó cân bằng:

Reconstruction
+
Latent regularization

Thường biểu diễn:

ELBO
=
reconstruction term
-
KL divergence

Đây là chỗ KL Divergence mà bạn hỏi trước đó xuất hiện rất tự nhiên.

32. GAN

GAN gồm:

Generator
      ↓
 fake image
      ↓
Discriminator
      ↑
 real image

Generator:

tạo ảnh giả.

Discriminator:

phân biệt thật/giả.

Hai network cạnh tranh.

Dùng:
image generation
image synthesis
style generation
33. DCGAN

DCGAN = GAN sử dụng convolutional architecture.

Nó là một model rất tốt để học:

GAN
+
CNN
Dùng:

Chủ yếu có giá trị học thuật/educational ngày nay.

34. Pix2Pix

Pix2Pix:

Image A
 ↓
Image B

Ví dụ:

edge map
 ↓
realistic image

hoặc:

sketch
 ↓
photo

Điểm quan trọng:

paired data

Bạn cần:

input image ↔ target image
35. CycleGAN

CycleGAN không yêu cầu paired data.

Ví dụ:

Horse → Zebra

Không cần:

horse image A
↔
zebra image A

Nó học hai chiều:

Horse → Zebra
Zebra → Horse

với cycle consistency.

Dùng:
style/domain translation
unpaired image translation
36. SRGAN

SRGAN = Super-Resolution GAN.

Low resolution
      ↓
     GAN
      ↓
High resolution
Dùng:
image super-resolution
image enhancement
37. StyleGAN / StyleGAN2 / StyleGAN3

StyleGAN là một dòng GAN cực kỳ quan trọng cho high-quality image generation.

Ý tưởng nổi bật:

control generation thông qua latent/style representations.

latent
 ↓
style
 ↓
Generator
 ↓
image

StyleGAN2 cải thiện quality/artifacts.

StyleGAN3 tập trung nhiều hơn vào các vấn đề liên quan đến aliasing và translation/rotation equivariance.

Dùng:
photorealistic image generation
synthetic faces
research về generative modeling
Diffusion

Đây là phần bạn nên học rất kỹ nếu muốn hiểu Stable Diffusion/Flux.

38. DDPM

DDPM = Denoising Diffusion Probabilistic Model.

Ý tưởng cực đẹp:

Forward diffusion

Lấy ảnh sạch:

x0
 ↓
add noise
 ↓
x1
 ↓
add noise
 ↓
x2
 ↓
...
 ↓
xT

Cuối cùng:

xT ≈ pure noise
Reverse diffusion

Model học:

noise
 ↓
remove noise
 ↓
less noise
 ↓
...
 ↓
image
xT → xT-1 → ... → x1 → x0

Đây là trái tim của diffusion.

39. DDIM

DDIM cải tiến sampling của DDPM.

Mục tiêu:

sinh ảnh với ít bước sampling hơn / trajectory khác.

Ví dụ:

DDPM:
1000 steps

DDIM:
50 steps

Tùy model/configuration.

Dùng:
faster sampling
deterministic-ish sampling
diffusion research
40. Latent Diffusion

Thay vì diffusion trực tiếp trên pixel:

Image
→ diffusion

làm:

Image
 ↓
VAE Encoder
 ↓
Latent
 ↓
Diffusion
 ↓
Latent
 ↓
VAE Decoder
 ↓
Image

Điều này giảm computation rất lớn.

Đây chính là ý tưởng nền tảng của Stable Diffusion.

41. Stable Diffusion

Một pipeline điển hình:

                Text
                 ↓
            Text Encoder
                 ↓
              Embedding
                 ↓
Noise → U-Net → Denoising
          ↑
       Text condition
                 ↓
              Latent
                 ↓
             VAE Decoder
                 ↓
               Image

Có thêm:

Scheduler

để điều khiển quá trình sampling.

42. CLIP trong Stable Diffusion

Trong các phiên bản Stable Diffusion đời đầu, CLIP-related text encoding đóng vai trò quan trọng trong text conditioning.

Nhưng cần phân biệt:

CLIP

là một vision-language model/alignment model,

trong khi:

Stable Diffusion

là một generative diffusion system.

43. Stable Diffusion XL

SDXL là thế hệ Stable Diffusion lớn hơn/mạnh hơn, với architecture và conditioning được cải thiện.

Dùng:
text-to-image
image-to-image
inpainting
high-quality generation
44. Flux

Flux là một dòng generative image model hiện đại, nổi bật với chất lượng text-to-image và khả năng render prompt phức tạp.

Điểm quan trọng về mặt học thuật:

Flux giúp bạn thấy hướng phát triển từ U-Net diffusion truyền thống sang các kiến trúc transformer-based hiện đại.

45. DiT

DiT = Diffusion Transformer.

Thay vì:

Diffusion
+
U-Net

dùng:

Diffusion
+
Transformer

Pipeline ý tưởng:

Noisy latent
 ↓
Transformer
 ↓
Predicted noise / velocity
 ↓
Scheduler
 ↓
Cleaner latent
Dùng:
generative image models
nghiên cứu diffusion transformer
46. Diffusion Transformer

Về cơ bản là hướng kiến trúc:

Diffusion process
+
Transformer architecture

DiT là một ví dụ tiêu biểu.

Ý tưởng lớn:

Transformer không chỉ dùng cho language; nó có thể trở thành backbone của generative vision.

47. Consistency Model

Diffusion thông thường:

noise
 ↓
step 1
 ↓
step 2
 ↓
...
 ↓
step 50
 ↓
image

Consistency Model hướng đến:

noise
 ↓
image

với rất ít bước.

Mục tiêu:

fast generation

48. Rectified Flow

Rectified Flow nhìn generative process theo hướng:

noise distribution
        ↓
    learn trajectory
        ↓
data distribution

Thay vì nhấn mạnh stochastic diffusion trajectory, nó học một vector field/flow để đưa noise về data.

Dùng:
modern generative modeling
efficient sampling
foundation image generation
49. Flow Matching

Flow Matching là framework để học:

vector field biến đổi một distribution thành distribution khác.

Có thể hình dung:

Noise
  ~~~~~~~
      \
       \
        → Data
             ████

Model học:

dx/dt = vθ(x,t)
Dùng:
generative modeling
diffusion alternatives
flow-based generation

Đây là một phần quan trọng để hiểu các hướng generative hiện đại.

Image Editing
50. Inpainting

Có vùng bị mask:

██████████
██      ██
██ MASK ██
██      ██
██████████

Model điền phần bị mất.

Dùng:
remove object
repair image
edit image
51. Outpainting

Ngược lại:

Original
████████

      ↓

████████████████
████ Original ████
████████████████

Mở rộng ảnh ra ngoài biên.

52. ControlNet

ControlNet cho phép kiểm soát diffusion bằng structure.

Ví dụ:

Canny edge
     ↓
ControlNet
     ↓
Stable Diffusion
     ↓
Image

Có thể control bằng:

edge
depth
pose
segmentation
sketch
Dùng:

Khi muốn:

"Sinh ảnh nhưng vẫn giữ cấu trúc này."

53. IP-Adapter

IP-Adapter dùng image prompt.

Thay vì chỉ:

Text → Image

có:

Text + Reference Image
          ↓
       Generation

Ví dụ:

reference person/style
          +
"person wearing..."
          ↓
       generated image
Dùng:
reference-guided generation
style/reference preservation
image-conditioned generation
54. DreamBooth

DreamBooth cho phép fine-tune model để học một subject cụ thể.

Ví dụ:

10–30 ảnh một subject
       ↓
 fine-tune
       ↓
model hiểu subject

Sau đó:

"subject X as astronaut"
Dùng:
personalization
subject-driven generation
55. Textual Inversion

Không fine-tune toàn bộ model.

Thay vào đó học một special token embedding.

<my_subject>

Model học:

<my_subject> ≈ concept X
Dùng:
personalized concepts
style/concept injection
Multimodal AI

Đây là tầng cao hơn:

Computer Vision
+
NLP
+
Reasoning
56. BLIP

BLIP = Bootstrapping Language-Image Pre-training.

Kết nối:

Image
 ↕
Language

Có thể làm:

image captioning
image-text matching
VQA
57. BLIP-2

BLIP-2 tìm cách kết nối:

Vision Encoder
      ↓
Q-Former
      ↓
LLM

Điểm rất quan trọng:

Không nhất thiết phải train lại toàn bộ vision encoder + LLM.

Dùng:
image understanding
VQA
captioning
multimodal reasoning
58. Flamingo

Flamingo nghiên cứu cách đưa visual information vào LLM để xử lý:

image
+
text
+
conversation

Đặc biệt đáng chú ý ở:

few-shot multimodal learning.

59. LLaVA

LLaVA là một kiến trúc rất dễ hiểu về multimodal LLM:

Image
 ↓
Vision Encoder
 ↓
Projection
 ↓
LLM
 ↑
Text

Ví dụ:

User:
[image]
"What is happening?"

        ↓

Vision Encoder
        ↓
Visual tokens
        ↓
LLM
        ↓
Answer
Dùng:
image chat
VQA
visual reasoning
60. Qwen-VL

Qwen-VL là dòng vision-language model tích hợp vision + language.

Có khả năng xử lý:

image understanding
OCR
grounding
visual question answering
document understanding

Đây là hướng rất gần với:

OCR + LLM
61. GPT-4o-style architecture

Ở mức ý tưởng, multimodal model hiện đại hướng tới:

Text
Image
Audio
Video
   ↓
Multimodal representation
   ↓
Large model
   ↓
Text / Audio / ...

Thay vì:

Vision model
+
LLM

rời rạc hoàn toàn.

Điểm cần hiểu ở đây không phải là chi tiết proprietary implementation, mà là:

một model có thể xử lý nhiều modality trong cùng một hệ thống.

62. Florence

Florence là dòng vision foundation model của Microsoft, hướng tới nhiều visual tasks:

image
 ↓
vision representation
 ↓
captioning
 ↓
detection
 ↓
grounding
 ↓
...

Nó thể hiện xu hướng:

một pretrained vision model phục vụ nhiều task.

63. Kosmos

Kosmos hướng tới multimodal perception + language, kết hợp vision với language understanding.

Một mục tiêu quan trọng là:

image
 ↓
perception
 ↓
language
 ↓
reasoning
64. Image Captioning

Task:

Image
 ↓
Model
 ↓
"A man is riding a bicycle."

Kiến trúc kinh điển:

CNN
 ↓
features
 ↓
RNN/LSTM
 ↓
text

Kiến trúc hiện đại:

Vision Transformer
 ↓
LLM
 ↓
caption
65. VQA

VQA = Visual Question Answering.

Image
+
Question
 ↓
Model
 ↓
Answer

Ví dụ:

Image: [kitchen]

Question:
"What color is the cup?"

Answer:
"Blue."
66. OCR + LLM

Đây là hướng rất đáng quan tâm với bạn.

Pipeline truyền thống:

Image
 ↓
OCR
 ↓
Text

Pipeline hiện đại:

Image
 ↓
Vision/OCR
 ↓
Text + Layout
 ↓
LLM
 ↓
Understanding

Ví dụ:

Invoice
 ↓
OCR
 ↓
{
  "date": "...",
  "total": "...",
  "company": "..."
}

LLM có thể thực hiện:

information extraction
document QA
classification
normalization
reasoning
structured JSON extraction
Cách mình khuyên bạn học toàn bộ danh sách này

Đừng học theo thứ tự bạn liệt kê.

Nếu mục tiêu của bạn là trở thành người hiểu sâu AI/CV, mình sẽ đi:

                 COMPUTER VISION
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   CNN basics      Classical CV    Geometry
        │              │              │
 LeNet/AlexNet    Edge/Threshold    Homography
        ↓          Contour/Feature   Calibration
 EfficientNet
 ConvNeXt
        │
        ↓
   Object Detection
        │
 SSD → RetinaNet → DETR
        │
        ↓
   Segmentation
        │
 FCN → U-Net → DeepLab
        │
 Mask R-CNN → SegFormer → SAM
        │
        ↓
      Pose
 OpenPose → HRNet
        │
        ↓
    Tracking
 KCF/CSRT → DeepSORT → ByteTrack

Sau đó đi nhánh OCR:

Image
 ↓
CNN
 ↓
CRNN
 ↓
CTC
 ↓
Transformer
 ↓
PaddleOCR
 ↓
Document AI
 ↓
OCR + LLM

Và song song:

              GENERATIVE AI
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
         VAE                 GAN
          │                   │
       ELBO/KL        DCGAN/Pix2Pix
                          │
                    CycleGAN/StyleGAN
          │
          └─────────┬─────────┘
                    ↓
                Diffusion
                    │
          ┌─────────┴──────────┐
          ↓                    ↓
        DDPM                  DDIM
          ↓                    ↓
   Latent Diffusion       Sampling
          ↓
 Stable Diffusion
          ↓
 SDXL
          ↓
 DiT / Flux
          ↓
 Flow Matching
 Rectified Flow

Cuối cùng:

Vision
   +
Language
   ↓
CLIP / SigLIP
   ↓
BLIP / BLIP-2
   ↓
Flamingo
   ↓
LLaVA / Qwen-VL
   ↓
Multimodal LLM
Nếu mục tiêu là hiểu bản chất, 15 model/khái niệm mình ưu tiên nhất là:

LeNet → AlexNet → ResNet (bạn đang thiếu cái này) → EfficientNet/ConvNeXt → SSD/RetinaNet → DETR → U-Net → Mask R-CNN → ViT → Swin → CRNN + CTC → CLIP → VAE → GAN → DDPM → Latent Diffusion → DiT → Multimodal LLM.

Đặc biệt, mình rất khuyên bổ sung ResNet vào danh sách của bạn. Nếu LeNet cho bạn hiểu CNN cơ bản, thì ResNet là model giúp bạn hiểu tại sao CNN có thể trở nên rất sâu, thông qua residual connection:

x
│
├───────────────┐
│               ↓
│            Conv
│               ↓
│            Conv
│               ↓
└──────────── (+)
                ↓
              F(x)+x

Nó là một trong những ý tưởng quan trọng nhất của Deep Learning hiện đại.