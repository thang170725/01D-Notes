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