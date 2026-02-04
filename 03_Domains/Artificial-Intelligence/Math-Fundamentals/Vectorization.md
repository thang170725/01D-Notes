Bag of Word (BoW)
    • Cho phân loại văn bản đơn giản → Không cần học sâu
    • Phù hợp khi cần nhanh, độ chính xác tương đối tốt, câu ngắn, cấu trúc cố định, từ vững rõ ràng.
    • Có thể sử dụng sklearn (CountVectorizer)
N-gram
    • Phổ biến với TF-IDF và BoW → Hiểu concept, không cần học sâu
    • Ý tưởng đơn giản: chia chuỗi ký tự/word thành các nhóm liên tiếp độ dài N.
        ◦ Unigram = từng token / từ riêng lẻ.
        ◦ Bigram = từng cặp từ liên tiếp.
        ◦ Trigram = bộ 3 từ liên tiếp.
    • nắm bắt ngữ cảnh cục bộ (ví dụ “New York” là bigram, có ý nghĩa khác so với hai từ riêng). Dùng trong: language modelling, feature cho classification, spelling correction, autocomplete.
    • Ví dụ dễ hiểu (word-level):
        ◦ Câu: “tôi yêu học AI”
        ◦ Unigrams: [“tôi”, “yêu”, “học”, “AI”]
        ◦ Bigrams: [“tôi yêu”, “yêu học”, “học AI”]
    • Ưu: đơn giản, hiệu quả cho nhiều task.
    • Nhược: số lượng feature bùng nổ khi N tăng; cần smoothing cho language model.
TF-IDF
    • Vẫn rất mạnh với các bài toán: spam, phân loại tin nhắn, search engine. → Quan trọng mức trung bình (chỉ cần hiểu công thức)
    • Ý tưởng đơn giản: tính trọng số cho từ dựa trên mức độ “quan trọng” của nó trong một document so với toàn bộ corpus.
        ◦ TF (term frequency): tần suất từ xuất hiện trong một tài liệu.
        ◦ IDF (inverse document frequency): giảm trọng số của từ xuất hiện ở nhiều tài liệu (ví dụ “và”, “the”).
    • vector hóa văn bản cho classification, search (retrieval), scoring (document ranking).
    • Ví dụ ngắn: Nếu “AI” xuất hiện nhiều trong một doc (TF cao) nhưng ít xuất hiện trong corpus (IDF cao) → TF-IDF cho “AI” lớn → từ quan trọng cho doc đó.
    • Ưu: đơn giản, hiệu quả cho văn bản ngắn và retrieval.
    • Nhược: bỏ qua thứ tự từ/ngữ cảnh; tính lạc hậu với embedding contextual.