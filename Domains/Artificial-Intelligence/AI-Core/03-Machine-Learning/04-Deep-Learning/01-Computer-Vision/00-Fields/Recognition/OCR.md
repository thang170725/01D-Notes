- [OCR Introduction (Optical Character Recognition - Là công nghệ nhận dạng ký tự quang học)](#ocr-introduction-optical-character-recognition---là-công-nghệ-nhận-dạng-ký-tự-quang-học)
- [Candidate (Thay vì chỉ trả về một đáp án duy nhất, mô hình thường giữ lại nhiều đáp án có xác suất cao nhất để xử lý tiếp)](#candidate-thay-vì-chỉ-trả-về-một-đáp-án-duy-nhất-mô-hình-thường-giữ-lại-nhiều-đáp-án-có-xác-suất-cao-nhất-để-xử-lý-tiếp)
- [Confidence (mức độ tự tin của model)](#confidence-mức-độ-tự-tin-của-model)
- [Quy trình hậu xử lý khi scan tài liệu bằng OCR](#quy-trình-hậu-xử-lý-khi-scan-tài-liệu-bằng-ocr)
  - [Tìm những từ nghi ngờ bị sai\*\*](#tìm-những-từ-nghi-ngờ-bị-sai)
    - [Phương pháp](#phương-pháp)
      - [Dictionary - Đánh dấu bằng từ điển (đơn giản nhất)](#dictionary---đánh-dấu-bằng-từ-điển-đơn-giản-nhất)
  - [Sinh Candidate (Candidate Generation - Với mỗi từ nghi ngờ, hãy tìm vài từ có khả năng là đáp áns)](#sinh-candidate-candidate-generation---với-mỗi-từ-nghi-ngờ-hãy-tìm-vài-từ-có-khả-năng-là-đáp-áns)
  - [Candidate Ranking (chọn candidate đúng nhất)](#candidate-ranking-chọn-candidate-đúng-nhất)
  - [Rule \& Business Logic](#rule--business-logic)
- [Ask (các câu hỏi liên quan đến OCR)](#ask-các-câu-hỏi-liên-quan-đến-ocr)
  - [mình không biết trước từ nào sẽ bị sai thì làm sao có vocab từ đúng để mà tính toán distance](#mình-không-biết-trước-từ-nào-sẽ-bị-sai-thì-làm-sao-có-vocab-từ-đúng-để-mà-tính-toán-distance)
  - [tôi tưởng Bert, phoBERT để hiểu ngữ cảnh, làm gì sửa trực tiếp được từ sai khi OCR](#tôi-tưởng-bert-phobert-để-hiểu-ngữ-cảnh-làm-gì-sửa-trực-tiếp-được-từ-sai-khi-ocr)
---
# OCR Introduction (Optical Character Recognition - Là công nghệ nhận dạng ký tự quang học)
```bash
Nó là một quá trình chuyển đổi hình ảnh chứa văn bản (chẳng hạn như tài liệu đã quét, ảnh chụp hoặc tệp PDF) thành văn bản mà máy tính có thể đọc, tìm kiếm và chỉnh sửa được.

Các ứng dụng phổ biến của OCR:
    - Chuyển đổi tài liệu giấy sang định dạng kỹ thuật số: Giúp dễ dàng lưu trữ, tìm kiếm và chỉnh sửa.
    - Trích xuất dữ liệu từ hóa đơn, biên lai, và các tài liệu khác: Tự động hóa việc nhập liệu.
    - Nhận dạng biển số xe: Sử dụng trong hệ thống giao thông thông minh.
    - Hỗ trợ người khiếm thị: Chuyển văn bản thành giọng nói.
    - Dịch thuật: Nhận dạng văn bản trong ảnh để dịch sang ngôn ngữ khác.
    - Tìm kiếm văn bản trong ảnh hoặc tệp PDF không tìm kiếm được.
```
**Quy trình OCR**
```bash
Ảnh (Tài liệu được quét hoặc chụp ảnh. Phần mềm OCR sẽ phân tích hình ảnh này, xác định các vùng sáng (nền) và vùng tối (văn bản))
   │
   ▼
Tiền xử lý ảnh (Hình ảnh được làm sạch và tối ưu hóa để cải thiện độ chính xác nhận dạng. Các bước này có thể bao gồm)
    - Chỉnh sửa độ nghiêng: Điều chỉnh lại hình ảnh nếu nó bị lệch khi quét.
    - Loại bỏ nhiễu: Xóa các điểm hoặc vệt không mong muốn trên hình ảnh.
    - Làm rõ nét: Tăng độ tương phản và làm sắc nét các ký tự.
    - Phân đoạn: Chia hình ảnh thành các dòng, từ và ký tự riêng lẻ.
   │
   ▼
OCR (PaddleOCR)
   │
   ▼
Text thô (có lỗi)
   │
   ▼
Tiền xử lý văn bản (Văn bản đã nhận dạng có thể được kiểm tra lỗi chính tả, ngữ pháp và định dạng lại cho phù hợp)
   │
   ▼
Sửa lỗi OCR
   │
   ▼
Kiểm tra theo ngữ cảnh
   │
   ▼
Kiểm tra theo quy tắc nghiệp vụ
   │
   ▼
Kết quả cuối cùng
```
# Candidate (Thay vì chỉ trả về một đáp án duy nhất, mô hình thường giữ lại nhiều đáp án có xác suất cao nhất để xử lý tiếp)
```bash
Ví dụ:
    Ảnh chứa từ: BAOVI

    Recognizer có thể dự đoán
        Candidate	Xác suất
        BAOVI	0.62
        BAOVN	0.18
        BAOVI	0.15
        BA0VI	0.05
```
**Candidate được sinh ra như thế nào?**
```bash
Điều này phụ thuộc vào mô hình OCR.
    1. Character Classification (OCR đời cũ)
        Mỗi ký tự được classifier dự đoán.

        Ví dụ
            Ảnh -> classifier

            Kết quả
                B : 99%
                8 : 1%
                A : 95%
                4 : 5%

    2. CTC-based OCR (CRNN, PaddleOCR)
        Đây là cách PaddleOCR hoạt động.

        Recognizer không dự đoán từng ký tự độc lập.
            Nó xuất ra một chuỗi xác suất theo thời gian.

        Ví dụ
            Time1
            B 0.95
            8 0.03
            R 0.02

            Time2
            A 0.70
            H 0.20
            4 0.10

            Time3
            O 0.80
            0 0.15
            Q 0.05

            Nếu chỉ lấy xác suất lớn nhất: B A O

            Nhưng thực tế còn tồn tại rất nhiều chuỗi khác
                BAO
                BHO
                8AO
                ...
        => Những chuỗi này chính là candidate.

    3. Transformer OCR (TrOCR, PARSeq)
        Mỗi bước sinh token
            Step1
                "B" 0.8
                "8" 0.1
                "R" 0.1

            Step2
                "A" 0.6
                "H" 0.3
                "4" 0.1
        Mỗi bước đều có nhiều lựa chọn.
        Candidate chính là các chuỗi được ghép từ các lựa chọn đó.
```
**Candidate được tạo bằng phương pháp gì?**
```bash
Có nhiều thuật toán.

1. Greedy Search (đơn giản nhất)
    Luôn lấy xác suất lớn nhất.

    Ví dụ
        B 0.9
        8 0.1
    → chọn B.

    Ưu điểm: nhanh
    
    Nhược điểm: dễ sai.

2. Beam Search ⭐ (phổ biến nhất)
    Không chỉ giữ một chuỗi. Mà giữ k chuỗi tốt nhất.

    Ví dụ
        Beam width = 3

    Sau bước đầu
        B 0.8
        8 0.15
        R 0.05

    Giữ
        B
        8
        R

    Sau bước hai
        BA
        BH
        8A
        RA
        ...

    Lại giữ 3 chuỗi tốt nhất.
    
    Beam Search gần như là tiêu chuẩn trong:
        - PaddleOCR
        - TrOCR
        - CRNN
        - PARSeq

Top-k Sampling
    Giữ k token có xác suất cao nhất.

    Ví dụ
        A 0.5
        H 0.2
        4 0.1
        X 0.1

    Top-3
        A
        H
        4

Hay dùng trong mô hình sinh văn bản hơn là OCR.

1. Language Model Rescoring

Sau khi có candidate

BAOVI
BAOVN
BAOVI

Dùng mô hình ngôn ngữ (BERT, GPT, n-gram...)

để chọn candidate hợp lý nhất.

Ví dụ

NHÜNG DIÈU CÀN LUU Ý

Recognizer tạo candidate

NHÜNG DIÈU CÀN LUU Ý
NHỮNG ĐIỀU CẦN LƯU Ý
NHỮNG ĐIỀU CẦN LUU Ý

Sau đó BERT đánh giá

P(sentence)

và chọn

NHỮNG ĐIỀU CẦN LƯU Ý

Đây chính là ý tưởng mình đã nhắc trong cuộc trao đổi trước: BERT không đọc ảnh, mà sửa lỗi trên các candidate văn bản do OCR sinh ra.

Với PaddleOCR thì candidate được tạo thế nào?

Pipeline đơn giản là:

Ảnh
    │
    ▼
Detection
    │
    ▼
Recognition
    │
    ▼
CTC Decoder
    │
    ├── Greedy Search (mặc định)
    │
    └── Beam Search (nếu bật)
    │
    ▼
Candidate text
    │
    ▼
Language Model (BERT, KenLM...)
    │
    ▼
Text cuối cùng

Nếu bạn đang dùng:

ocr = PaddleOCR()

thì mặc định thường CTC Greedy Decoder được sử dụng, tức là mô hình chỉ lấy chuỗi có xác suất cao nhất và không giữ nhiều candidate.

Nếu mục tiêu của bạn là kết hợp PaddleOCR với BERT để sửa lỗi OCR, thì bạn cần tạo hoặc truy xuất nhiều candidate (ví dụ bằng CTC Beam Search) rồi dùng BERT hoặc một language model để chấm điểm và chọn câu hợp lý nhất. Đây là quy trình phổ biến trong các hệ thống OCR hiện đại khi cần tăng độ chính xác trên văn bản tiếng Việt.
```
# Confidence (mức độ tự tin của model) 
# Quy trình hậu xử lý khi scan tài liệu bằng OCR
**Tại sao hậu xử lý?**
```bash
Sau khi OCR sẽ có rất nhiều lỗi ta cần hậu xử lý.
```
## Tìm những từ nghi ngờ bị sai**
```bash
Mục tiêu KHÔNG phải là sửa. Mà là trả lời câu hỏi:
    Trong hàng trăm dòng OCR này, dòng nào đáng nghi?

Ví dụ
    BAOVIET
    Insurance
    0966.795.333
    => khả năng rất cao là đúng.

    Trong khi
        NHÜNG DIÈU CÀN LUU Ý
    => nhìn đã thấy sai rất nhiều.
```
### Phương pháp
```bash
Giả sử OCR trả về:
    NHÜNG DIÈU CÀN LUU Ý

Máy sẽ tách từ:
    NHÜNG
    DIÈU
    CÀN
    LUU
    Ý

=> Bây giờ mục tiêu là: Trong 5 từ này, từ nào đáng nghi?
```
#### Dictionary - Đánh dấu bằng từ điển (đơn giản nhất)
```bash
Giả sử có từ điển:
    - NHỮNG
    - ĐIỀU
    - CẦN
    - LƯU
    - Ý

Kiểm tra:
    | Từ OCR | Có trong từ điển? |
    | ------ | ----------------- |
    | NHÜNG  | ❌                |
    | DIÈU   | ❌                |
    | CÀN    | ❌                |
    | LUU    | ❌                |
    | Ý      | ✅                |

=> đánh dấu 4 từ
```
**Nhược điểm**
```bash
Nhưng...
    Đây là lúc bạn sẽ hỏi ngay:
        "Nếu OCR đọc GIAY thì sao? GIAY cũng có thể không có trong từ điển."
            Hoặc
        Duy Mong -> Tên người. Dictionary cũng không có.
=> Vậy dictionary không đủ.

Vì vậy doanh nghiệp thường dùng nhiều tín hiệu cùng lúc.
    Ví dụ một từ sẽ được chấm điểm.
        Tiêu chí	            Ví dụ
        Confidence OCR thấp?	✅
        Không có trong từ điển?	✅
        Có ký tự lạ (Ü, Ä, È)?	✅
        Ngữ cảnh bất thường?	✅

Ví dụ
    NHÜNG
        Có:
            - Confidence 0.41
            - Có ký tự Ü
            - Không có trong từ điển
            => Khả năng sai rất cao.

    BAOVIET
        - Confidence 1.00
        - Không có trong từ điển tiếng Việt
        - Nhưng:
            + Toàn chữ in hoa
            + Có trong danh sách tên thương hiệu
        => Không sửa.
```
## Sinh Candidate (Candidate Generation - Với mỗi từ nghi ngờ, hãy tìm vài từ có khả năng là đáp áns)
```bash
Ví dụ:
    Với từ "NHÜNG". Hệ thống tìm các từ gần giống.
        - NHỮNG
        - NHƯNG
        - NHUNG
        - NHŨNG
        => Đây gọi là candidate (ứng viên).

Lưu ý:
    Không tìm trong toàn bộ hàng triệu từ, mà chỉ sinh ra một vài ứng viên có khả năng nhất.
```
**Candidate được sinh bằng gì?**
```bash
Có 2 cách
    - Nếu dùng Edit Distance, BK-Tree, SymSpell, Trie thì đúng là phải có vocabulary.
    - Nếu dùng LLM hoặc mô hình sinh - generative model thì có thể không cần vocabulary vì model sinh trực tiếp từ đúng.
```
```bash
Đây là lúc các thuật toán như:
    - Edit Distance
    - SymSpell
    - BK-Tree
    - Trie
mới xuất hiện.

Ví dụ Edit Distance.
    GIAY và GIẤY chỉ khác dấu. Distance = nhỏ. => thêm vào candidate.

"Nếu có hàng triệu từ thì sao?"
    Không ai làm thế này:
        for word in 2_000_000_words:
            distance(ocr_word, word)
    => Vì quá chậm.

Thay vào đó, người ta xây trước cấu trúc dữ liệu (BK-Tree, SymSpell, Trie...) để truy xuất rất nhanh các từ gần giống.

Giống như từ điển trong điện thoại.
    Bạn gõ: ngy
        Điện thoại gần như lập tức gợi ý: ngày
    
    Nó không duyệt toàn bộ từ điển tiếng Việt mỗi lần bạn gõ.
```
## Candidate Ranking (chọn candidate đúng nhất)
```bash
Ví dụ:
    OCR đọc: GIAY CHUNG NHAN

    Candidate:
        GIAY
        ↓
        1. GIẤY
        2. GIÀY
        3. GIẢY

        CHUNG
        ↓
        1. CHỨNG
        2. CHUNG

        NHAN
        ↓
        1. NHẬN
        2. NHÂN
        3. NHÁN

Bây giờ hệ thống có rất nhiều cách kết hợp.
    Ví dụ:
        - GIẤY CHỨNG NHẬN
        - GIẤY CHUNG NHÂN
        - GIÀY CHỨNG NHẬN
        - GIÀY CHUNG NHÂN
        - ...
=> Câu hỏi là: chọn câu nào? Đây mới là lúc BERT/PhoBERT xuất hiện.

Lưu ý:
    - PhoBERT không sửa từ.
    - PhoBERT chỉ trả lời:
    -     "Trong các câu này, câu nào tự nhiên nhất?"

Ví dụ:
    Câu A: GIẤY CHỨNG NHẬN
        phoBERT: Điểm: 0.99
    
    Câu B: GIÀY CHỨNG NHẬN
        PhoBERT: Điểm: 0.02

    Câu C: GIẢY CHỨNG NHÂN
        PhoBERT: Điểm: 0.01

PhoBERT làm điều này như thế nào?
    Đây chính là chỗ bạn hỏi: "Nếu đưa câu sai vào thì embedding vẫn sai mà?"

    PhoBERT không nhìn một từ. Nó nhìn toàn bộ câu.

    Ví dụ: GIAY CHUNG NHAN
        Sau khi sinh candidate:
            - GIẤY CHỨNG NHẬN
            - GIÀY CHỨNG NHẬN

    Hai câu này đều được đưa qua PhoBERT.
        PhoBERT tạo embedding cho cả câu.

    Nếu trong quá trình huấn luyện, nó đã đọc hàng triệu câu tiếng Việt, thì nó biết:
        - GIẤY CHỨNG NHẬN => là một cụm xuất hiện rất nhiều.
        - Còn GIÀY CHỨNG NHẬN => gần như chưa bao giờ xuất hiện.
    => Nên embedding của câu thứ nhất sẽ được đánh giá "tự nhiên" hơn.

Một lưu ý rất quan trọng
    Có một câu mình muốn sửa lại từ các tin nhắn trước để tránh bạn hiểu sai.

    Mình từng nói: PhoBERT cho điểm câu.
        Thực ra PhoBERT nguyên bản không tự cho điểm.

        Đúng hơn là:
            Candidate Sentence
                    │
                    ▼
            PhoBERT
                    │
            Sinh embedding
                    ▼
            Classifier / Scoring Head
                    ▼
            Score

    Tức là PhoBERT + một head được huấn luyện mới tạo ra điểm. PhoBERT chỉ cung cấp đặc trưng (embedding).
```
## Rule & Business Logic
```bash
Giả sử hệ thống đã sửa được: GIẤY CHỨNG NHẬN ==> rất tốt.

Nhưng đến đây vẫn chưa kết thúc.
    Vì AI vẫn có thể sửa sai.

Ví dụ 1
    OCR Số tiền bảo hiểm: ..10.00.000.

    Candidate
        - 10.000.000
        - 10.100.000

    PhoBERT gần như không biết số nào đúng.

    Nhưng rule có thể biết.

Ví dụ:
    Số tiền bảo hiểm phải là bội số của 1.000
        hoặc
    Định dạng tiền phải là 10.000.000
=> Rule thắng AI.

Ví dụ 2
    OCR Ngày 18../04../2019 
    
    AI có thể đoán 18/04/2019

    Nhưng nếu OCR đọc 39/18/2019

    AI vẫn có thể sinh lung tung.

    Rule biết ngay 39 không phải ngày hợp lệ.

Ví dụ 3
    OCR: Website www.bsoviel.com.vn

    AI có thể sửa thành www.baoviet.com.vn

    Nhưng nếu doanh nghiệp có database
    Website chính thức www.baoviet.com.vn
=> Rule sửa chính xác.

Ví dụ gần với tài liệu của bạn
    OCR: BÃO HIM BÃO VIT

    Candidate
        BẢO HIỂM BẢO VIỆT
        BÃO HIM BÃO VIT
        BẢO HIẾM BÁO VIỆT

    PhoBERT có thể chọn đúng. Nhưng công ty còn có Rule
        Tên công ty luôn là "BẢO HIỂM BẢO VIỆT"
    => Chắc chắn đúng.

Vì sao Rule vẫn rất quan trọng?
    Một câu mình muốn bạn nhớ: AI giỏi ngôn ngữ. Rule giỏi nghiệp vụ.

    Ví dụ:
        OCR: Số hợp đồng 0333869/TNCN/16

        AI không nên sửa. Rule biết Mã hợp đồng có format: xxxxxxx/TNCN/xx => giữ nguyên.
```
# Ask (các câu hỏi liên quan đến OCR)
## mình không biết trước từ nào sẽ bị sai thì làm sao có vocab từ đúng để mà tính toán distance
```bash
Trường hợp 1: OCR tiếng Việt tổng quát
    Ví dụ OCR đọc: GIAY CHUNG NHAN BAO HIEM

    Hệ thống không biết trước từ nào sẽ sai. Nhưng nó luôn có một vocabulary.
        Vocabulary này có thể là:

    Toàn bộ từ trong từ điển tiếng Việt (VnCoreNLP, Vspell, Wiktionary...)
        Hàng trăm nghìn từ được thống kê từ báo chí, sách, Wikipedia...
        Từ vựng chuyên ngành nếu là hóa đơn, bảo hiểm, ngân hàng...

    Ví dụ:
        GIẤY
        CHỨNG
        NHẬN
        BẢO
        HIỂM
        ...
        500.000 từ khác

    Đây là dữ liệu được chuẩn bị trước khi hệ thống chạy, chứ không sinh ra từ ảnh.

Trường hợp 2: Từ không có trong từ điển
    Ví dụ OCR đọc: Nguyễn Văn Xyzabc hoặc Công ty ABC123

    Nếu dùng từ điển thì sẽ coi là sai. Nhưng thực tế nó lại đúng.
    => Đây chính là lý do không doanh nghiệp nào chỉ dùng dictionary.

    Vì vậy hệ thống thực tế sẽ như thế này
        Ví dụ OCR: GIAY CHUNG NHAN BAO HIEM
        Không phải cứ thấy GIAY

    không có trong từ điển là sửa ngay.
        Mà sẽ hỏi thêm:
            - Confidence của OCR là bao nhiêu?
            - Đây là tiêu đề hay tên riêng?
            - Có nằm trong ngữ cảnh "GIAY CHUNG NHAN" không?
            - Đây có phải tài liệu bảo hiểm không?
            - Quan trọng hơn: Có nhiều hệ thống không dùng vocabulary để sinh candidate

Ví dụ dùng Transformer hoặc LLM.

OCR đọc:

GIAY CHUNG NHAN

Model nhận cả câu:

GIAY CHUNG NHAN

↓

Sinh luôn

GIẤY CHỨNG NHẬN

Nó không cần duyệt từng từ trong từ điển.

Đây giống bài toán sequence-to-sequence hơn là spell checking.

Một ví dụ thực tế

Google Docs OCR.

OCR đọc:

Cong hoa xa hoi chu nghia Viet Nam

Nó sửa thành

Cộng hòa xã hội chủ nghĩa Việt Nam

Google không ngồi tính edit distance với từng từ trong hàng triệu từ.

Họ dùng mô hình ngôn ngữ đã được huấn luyện trên lượng văn bản khổng lồ để dự đoán câu nào hợp lý nhất.

Anh phỏng vấn nói về embedding thì sao?

Đây là điều mình nghi ngờ nhất.

Nếu anh ấy nói:

"So sánh embedding của từ OCR sai với từ đúng."

thì rất có thể anh ấy không mô tả toàn bộ hệ thống, mà chỉ đang nói về một bước trong pipeline.

Vì đúng như bạn phân tích:

Nếu không có vocabulary thì không thể tìm theo edit distance.
Nếu vocabulary quá lớn thì không thể so sánh tuần tự từng từ.
Nếu có tên riêng, địa chỉ, mã sản phẩm... thì dictionary sẽ thất bại.

Do đó, trong các hệ thống hiện đại, người ta thường kết hợp nhiều nguồn thông tin:

Từ điển cho các từ phổ biến.
Mô hình ngôn ngữ để hiểu ngữ cảnh.
Rule theo từng loại tài liệu.
Danh sách tên riêng hoặc thuật ngữ chuyên ngành nếu cần.
Theo mình, có một câu bạn nên hỏi lại chính anh phỏng vấn nếu có cơ hội:

"Anh sinh candidate như thế nào trước khi so sánh embedding? Hay anh encode toàn bộ vocabulary vào vector database rồi tìm nearest neighbor?"

Đây là câu hỏi rất kỹ thuật.

Nếu họ thực sự dùng embedding để sửa OCR, họ sẽ phải có một cơ chế sinh hoặc truy xuất candidate trước. Câu trả lời của họ sẽ cho bạn biết họ đang dùng:

Dictionary + BK-Tree/SymSpell,
FAISS/Milvus với embedding,
hay LLM/Transformer để sửa trực tiếp.

Đó mới là phần quyết định kiến trúc của hệ thống. Chỉ nói "so sánh embedding" thì vẫn còn thiếu một mắt xích quan trọng trong pipeline.

nhưng nếu vứt lên LLM thế để sửa tù sai thì mình sẽ vô tình làm lộ thông tin, vậy phải làm như nào
Đây là một câu hỏi rất thực tế. Và đúng là nhiều doanh nghiệp (đặc biệt ngân hàng, bảo hiểm, bệnh viện) không được phép gửi dữ liệu OCR lên ChatGPT hay API của bên thứ ba vì lý do bảo mật.

Vậy họ làm thế nào?

Cách 1. Chạy LLM nội bộ (On-premise) ⭐⭐⭐⭐⭐

Đây là cách phổ biến nhất.

Pipeline:

Ảnh
    ↓
PaddleOCR
    ↓
Text OCR
    ↓
Llama 3 / Qwen / Gemma (chạy trong server công ty)
    ↓
Text đã sửa

Dữ liệu không bao giờ ra khỏi công ty.

Ví dụ:

Ngân hàng
Bệnh viện
Cơ quan nhà nước

thường triển khai LLM trên máy chủ hoặc GPU của chính họ.

Cách 2. Không dùng LLM, chỉ dùng mô hình nhỏ

Ví dụ:

OCR
    ↓
Dictionary
    ↓
Language Model
    ↓
Rule

Language Model ở đây có thể là:

PhoBERT
BERT
RoBERTa
BiLSTM
Transformer nhỏ

Chúng chỉ làm nhiệm vụ sửa lỗi chính tả hoặc đánh giá ngữ cảnh, không cần LLM cỡ lớn.

Cách 3. Chỉ gửi một phần dữ liệu

Ví dụ OCR ra:

Tên:
Nguyễn Văn A

CCCD:
012345678901

Địa chỉ:
123 Lê Lợi

NHÜNG DIÈU CÀN LUU Ý

Hệ thống sẽ che dữ liệu nhạy cảm trước:

Tên:
[PERSON]

CCCD:
[ID]

Địa chỉ:
[ADDRESS]

NHÜNG DIÈU CÀN LUU Ý

Sau đó mới gửi phần cần sửa.

Đây gọi là PII Masking (ẩn thông tin nhận dạng cá nhân).

Cách 4. Chỉ sửa những vùng nghi ngờ

Ví dụ OCR:

GIẤY CHỨNG NHẬN

confidence:

GIẤY      0.99
CHỨNG     0.98
NHẬN      0.99

Không cần sửa.

Nhưng

NHÜNG

confidence

0.35

Chỉ gửi đúng từ hoặc đúng dòng này sang mô hình sửa lỗi.

Không gửi toàn bộ tài liệu.

Doanh nghiệp lớn thường làm gì?

Ví dụ ngân hàng.

Ảnh CCCD
       ↓
OCR
       ↓
Rule Validation
       ↓
NER (tìm thông tin nhạy cảm)
       ↓
Mask dữ liệu
       ↓
LLM nội bộ
       ↓
JSON

Hoặc thậm chí:

OCR
      ↓
PhoBERT
      ↓
Rule

Không dùng LLM luôn.

Nếu là ChatGPT API thì sao?

Nhiều công ty không cho phép gửi:

CCCD
Hộ chiếu
Hồ sơ bệnh án
Hợp đồng
Thông tin khách hàng

lên dịch vụ AI bên ngoài nếu chưa được ẩn danh hoặc chưa có thỏa thuận xử lý dữ liệu phù hợp.

Vì vậy họ sẽ:

tự host model,
hoặc dùng dịch vụ AI có cam kết bảo mật phù hợp,
hoặc chỉ gửi dữ liệu đã được ẩn thông tin.
Nếu bạn đi phỏng vấn

Nếu người phỏng vấn hỏi:

"Em sửa OCR bằng LLM thế nào?"

Một câu trả lời khá tốt sẽ là:

"Nếu dữ liệu không nhạy cảm thì có thể dùng API của LLM để hậu xử lý. Tuy nhiên với tài liệu như CCCD, hồ sơ bệnh án hoặc hợp đồng, em sẽ ưu tiên chạy LLM nội bộ hoặc dùng các mô hình nhỏ như PhoBERT kết hợp rule-based để tránh rò rỉ dữ liệu."

Đó là câu trả lời thể hiện rằng bạn không chỉ biết về AI mà còn hiểu các yêu cầu thực tế về bảo mật và triển khai trong doanh nghiệp.
```
## tôi tưởng Bert, phoBERT để hiểu ngữ cảnh, làm gì sửa trực tiếp được từ sai khi OCR
```bash
BERT/PhoBERT bản gốc không phải là mô hình sửa lỗi chính tả.
    Nó là encoder, nhiệm vụ chính là:
        - sinh embedding
        - hiểu ngữ cảnh
        - phục vụ các task như classification, NER, QA...

    Nó không tự sinh ra câu mới như ChatGPT.

PhoBERT làm gì?
    Ví dụ: Tôi đang học OCR.

    PhoBERT sẽ biến thành
        Tôi      → vector 768 chiều
        đang     → vector 768 chiều
        học      → vector 768 chiều
        OCR      → vector 768 chiều
    Nó dừng ở đây.
```
**Vậy tại sao nhiều bài báo nói dùng BERT để sửa lỗi?**
```bash
Vì họ không dùng PhoBERT nguyên bản.

Họ thêm một "đầu ra" (head) lên trên PhoBERT.
    Ví dụ
        Input
        ↓     
        PhoBERT
        ↓
        Linear Layer
        ↓
        Softmax
        ↓
        Predict từ đúng

    Giống như YOLO. YOLO backbone chỉ trích xuất feature. Đầu Detect Head mới dự đoán: người, xe, chó

Ví dụ cụ thể
    Input: NHUNG ĐIỀU CẦN LƯU Ý

    PhoBERT encode
    ↓
    vector
    ↓
    Classifier
    ↓
    Predict
=> Tức là mô hình đã được fine-tune cho bài toán sửa lỗi. Không phải PhoBERT tự sửa.
```
**Nếu đưa câu sai vào thì sao?**
```bash
Ví dụ: GIAY CHUNG NHAN
    PhoBERT vẫn sinh embedding.

    Vì embedding phụ thuộc vào toàn bộ câu.
        Embedding của GIAY sẽ gần với GIẤY hơn là GIÀY
            vì phía sau là CHUNG NHAN

    Mô hình học được rằng "GIẤY CHỨNG NHẬN" là cụm cực kỳ phổ biến.

Nhưng PhoBERT có tự sửa được không?
    Không.

    PhoBERT chỉ nói embedding của từ này trong ngữ cảnh này giống embedding của "GIẤY" hơn.

    Việc quyết định
        GIAY
        ↓
        GIẤY

    phải có thêm
        - classifier
        - decoder
        - CRF
        - seq2seq
    tùy kiến trúc.

Nếu muốn mô hình tự sinh câu đúng Thì phải dùng encoder-decoder hoặc decoder-only.

Ví dụ
    Input: GIAY CHUNG NHAN
    ↓
    mT5
    ↓
    Output: GIẤY CHỨNG NHẬN

    hoặc

    LLama
    ↓
    GIẤY CHỨNG NHẬN
=> Đây mới là mô hình "sinh" văn bản.
```