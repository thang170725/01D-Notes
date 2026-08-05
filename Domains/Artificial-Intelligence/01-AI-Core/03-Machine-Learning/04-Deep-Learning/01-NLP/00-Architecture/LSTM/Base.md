- [Introduction](#introduction)
- [Practices](#practices)
  - [Research LSTM](#research-lstm)
---
# Introduction
```bash
LSTM (Long Short-Term Memory) giải quyết việc mất trí nhớ của RNN.

LSTM tách biệt hoàn toàn hai khái niệm: 
    - Hidden State (trạng thái ẩn) 
    - Cell State (trạng thái ô - đóng vai trò như một đường băng chuyền thông tin xuyên suốt). 
    - Thêm cấu trúc “cổng” (gate) và có cell state giúp duy trì thông tin dài hạn.

Cơ chế 3 Cổng (Gates): Hãy tưởng tượng Cell State là một băng tải chạy dọc từ đầu đến cuối chuỗi.\n Các cổng sẽ quyết định cái gì được đặt lên hoặc nhấc ra khỏi băng tải đó:
    - Forget Gate (Cổng quên): "Chúng ta nên bỏ bớt cái gì cũ không?"
        + Nó nhận đầu vào xt​ và ht−1​, đi qua hàm Sigmoid (cho ra giá trị từ 0 đến 1).
        + Nếu là 0: Xóa bỏ hoàn toàn thông tin cũ. Nếu là 1: Giữ lại toàn bộ.
    - Input Gate (Cổng vào): "Có thông tin mới nào đáng giá để lưu lại không?"
        + Gồm 2 phần: 
            - Một hàm Sigmoid quyết định cập nhật cái gì 
            - một hàm tanh tạo ra một vector giá trị mới tiềm năng để đưa vào Cell State.
    - Output Gate (Cổng ra): "Từ những gì đang có, chúng ta nên xuất bản cái gì ra ngoài?"
        + Nó quyết định giá trị nào trong Cell State sẽ được dùng để tạo ra Hidden State (ht​) cho bước tiếp theo. 

Ưu điểm: Nhớ được thông tin xa hơn, Giảm vanishing gradient, Ổn định hơn khi xử lý văn bản dài
```
# Practices
## Research LSTM
```python
import torch
import torch.nn as nn


class CustomLSTMCell(nn.Module):
    """
    Xây dựng một LSTM Cell đơn lẻ (xử lý dữ liệu tại 1 bước thời gian t)
    Sử dụng thuần túy các công thức toán học.
    """

    def __init__(self, input_size: int, hidden_size: int):
        super(CustomLSTMCell, self).__init__()
        self.input_size = input_size
        self.hidden_size = hidden_size

        # --- KHỞI TẠO TRỌNG SỐ CHO CẢ 4 CỔNG (Forget, Input, Cell-candidate, Output) ---
        # Gom trọng số lại thành một ma trận lớn (4 * hidden_size, ...) để tính toán song song nhanh hơn
        self.W_x = nn.Parameter(torch.randn(4 * hidden_size, input_size) * 0.1)
        self.W_h = nn.Parameter(torch.randn(4 * hidden_size, hidden_size) * 0.1)
        self.b = nn.Parameter(torch.zeros(4 * hidden_size))

    def forward(self, x_t: torch.Tensor, h_prev: torch.Tensor, c_prev: torch.Tensor):
        """
        Forward qua 1 Cell tại thời điểm t.
        x_t: (batch_size, input_size)
        h_prev: (batch_size, hidden_size) - trạng thái ẩn ẩn trước đó
        c_prev: (batch_size, hidden_size) - trạng thái ô (cell state) trước đó
        """
        # 1. Nhân ma trận song song cho cả 4 cổng: Z = X*W_x^T + H*W_h^T + b
        gates = torch.matmul(x_t, self.W_x.t()) + torch.matmul(h_prev, self.W_h.t()) + self.b
        
        # 2. Tách ma trận kết quả thành 4 phần bằng nhau tương ứng với 4 cổng
        f_gate, i_gate, g_gate, o_gate = torch.chunk(gates, 4, dim=1)

        # 3. Áp dụng các hàm kích hoạt (Activation Functions)
        f = torch.sigmoid(f_gate)  # Forget gate: Quyết định quên bao nhiêu dữ liệu cũ
        i = torch.sigmoid(i_gate)  # Input gate: Quyết định nạp bao nhiêu dữ liệu mới vào
        g = torch.tanh(g_gate)     # Cell candidate: Nội dung thông tin mới muốn nạp
        o = torch.sigmoid(o_gate)  # Output gate: Quyết định xuất bao nhiêu thông tin ra Hidden State

        # 4. Cập nhật Cell State (Trạng thái ô): c_t = f * c_prev + i * g
        c_t = f * c_prev + i * g

        # 5. Cập nhật Hidden State (Trạng thái ẩn): h_t = o * tanh(c_t)
        h_t = o * torch.tanh(c_t)

        return h_t, c_t, (f, i, g, o)


class LSTMResearchNetwork(nn.Module):
    """
    Mô phỏng một Layer LSTM xử lý chuỗi dữ liệu dài qua nhiều bước thời gian.
    Tích hợp Log hệ thống để theo dõi Workflow dữ liệu.
    """

    def __init__(self, input_size: int, hidden_size: int):
        super(LSTMResearchNetwork, self).__init__()
        self.hidden_size = hidden_size
        self.lstm_cell = CustomLSTMCell(input_size, hidden_size)

    def forward(self, x_sequence: torch.Tensor):
        """
        x_sequence: (batch_size, seq_len, input_size)
        """
        batch_size, seq_len, input_size = x_sequence.size()

        # Khởi tạo trạng thái ban đầu h_0 và c_0 bằng 0
        h_t = torch.zeros(batch_size, self.hidden_size, device=x_sequence.device)
        c_t = torch.zeros(batch_size, self.hidden_size, device=x_sequence.device)

        # Danh sách lưu lại output qua từng bước thời gian
        outputs = []

        print(f"=== BẮT ĐẦU LUỒNG XỬ LÝ LSTM (Batch Size: {batch_size}, Chiều dài chuỗi: {seq_len}) ===")
        print(f" Kích thước vector đầu vào mỗi timestep: {input_size} | Kích thước Hidden State: {self.hidden_size}\n")

        # Duyệt dọc theo trục thời gian (Time-steps Loop)
        for t in range(seq_len):
            print(f"⏱️ [TIME STEP t = {t}]")
            
            # Trích xuất dữ liệu của tất cả các mẫu tại thời điểm t
            x_t = x_sequence[:, t, :]
            print(f"  -> Input x_t kích thước: {list(x_t.shape)} | Giá trị mẫu đầu tiên: {x_t[0].tolist()}")

            # Đưa vào Cell xử lý toán học thuần túy
            h_t, c_t, (f, i, g, o) = self.lstm_cell(x_t, h_t, c_t)

            # Log thông số các cổng của mẫu dữ liệu đầu tiên để debug toán học
            print(f"  [Cổng Forget f] Giữ lại: {f[0].mean().item()*100:.1f}% thông tin cũ.")
            print(f"  [Cổng Input  i] Cho phép: {i[0].mean().item()*100:.1f}% thông tin mới đi vào.")
            print(f"  [Ứng viên    g] Giá trị thông tin mới đề xuất (mean): {g[0].mean().item():.3f}")
            print(f"  [Cổng Output o] Cho phép: {o[0].mean().item()*100:.1f}% Cell state xuất ra Hidden state.")
            print(f"  💾 Cell State c_t mới (mẫu 1): {c_t[0].tolist()}")
            print(f"  🧠 Hidden State h_t mới (mẫu 1): {h_t[0].tolist()}\n")

            outputs.append(h_t.unsqueeze(1))

        # Gom tất cả các output lại thành tensor cấu trúc: (batch_size, seq_len, hidden_size)
        outputs = torch.cat(outputs, dim=1)
        return outputs, (h_t, c_t)


# --- CHẠY THỬ NGHIỆM ĐỂ QUAN SÁT LOG ---
if __name__ == "__main__":
    # Cố định seed để các trọng số ngẫu nhiên không đổi khi chạy lại
    torch.manual_seed(42)

    # Giả lập bài toán NLP hoặc chuỗi thời gian: 
    # Giả sử ta có Batch gồm 2 câu (batch_size=2), mỗi câu có 3 từ (seq_len=3), mỗi từ biến thành vector 4 chiều (input_size=4)
    B_SIZE = 2
    S_LEN = 3
    IN_SIZE = 4
    H_SIZE = 2  # Cấu hình hidden_size nhỏ (=2) để log in ra màn hình gọn gàng, dễ soi số liệu

    dummy_input = torch.randn(B_SIZE, S_LEN, IN_SIZE)

    # Khởi tạo mô hình nghiên cứu
    lstm_net = LSTMResearchNetwork(input_size=IN_SIZE, hidden_size=H_SIZE)
    
    # Thực thi Forward pass
    final_outputs, (last_h, last_c) = lstm_net(dummy_input)

    print("=" * 70)
    print("[KẾT QUẢ CUỐI CÙNG HOÀN THÀNH PIPELINE]")
    print(f"Kích thước tensor đầu ra tổng thể (outputs): {list(final_outputs.shape)}")
    print(f"Kích thước Hidden State cuối cùng: {list(last_h.shape)}")
```
```bash
=== BẮT ĐẦU LUỒNG XỬ LÝ LSTM (Batch Size: 2, Chiều dài chuỗi: 3) ===
 Kích thước vector đầu vào mỗi timestep: 4 | Kích thước Hidden State: 2

⏱️ [TIME STEP t = 0]
  -> Input x_t kích thước: [2, 4] | Giá trị mẫu đầu tiên: [1.9269152879714966, 1.4872840642929077, 0.9007171988487244, -2.1055209636688232]
  [Cổng Forget f] Giữ lại: 58.7% thông tin cũ.
  [Cổng Input  i] Cho phép: 46.4% thông tin mới đi vào.
  [Ứng viên    g] Giá trị thông tin mới đề xuất (mean): 0.069
  [Cổng Output o] Cho phép: 51.2% Cell state xuất ra Hidden state.
  💾 Cell State c_t mới (mẫu 1): [-0.058885976672172546, 0.17608407139778137]
  🧠 Hidden State h_t mới (mẫu 1): [-0.024512547999620438, 0.10566490888595581]

⏱️ [TIME STEP t = 1]
  -> Input x_t kích thước: [2, 4] | Giá trị mẫu đầu tiên: [0.6784184575080872, -1.2345448732376099, -0.04306747764348984, -1.6046669483184814]
  [Cổng Forget f] Giữ lại: 52.0% thông tin cũ.
  [Cổng Input  i] Cho phép: 47.4% thông tin mới đi vào.
  [Ứng viên    g] Giá trị thông tin mới đề xuất (mean): 0.047
  [Cổng Output o] Cho phép: 49.0% Cell state xuất ra Hidden state.
  💾 Cell State c_t mới (mẫu 1): [-0.023509366437792778, 0.1343829482793808]
  🧠 Hidden State h_t mới (mẫu 1): [-0.010362068191170692, 0.07195575535297394]

⏱️ [TIME STEP t = 2]
  -> Input x_t kích thước: [2, 4] | Giá trị mẫu đầu tiên: [0.3558599054813385, -0.6866229772567749, -0.4933563470840454, 0.2414877861738205]
  [Cổng Forget f] Giữ lại: 49.1% thông tin cũ.
  [Cổng Input  i] Cho phép: 50.7% thông tin mới đi vào.
  [Ứng viên    g] Giá trị thông tin mới đề xuất (mean): -0.063
  [Cổng Output o] Cho phép: 50.0% Cell state xuất ra Hidden state.
  💾 Cell State c_t mới (mẫu 1): [-0.036286771297454834, 0.029130350798368454]
  🧠 Hidden State h_t mới (mẫu 1): [-0.017979558557271957, 0.014698137529194355]

======================================================================
[KẾT QUẢ CUỐI CÙNG HOÀN THÀNH PIPELINE]
Kích thước tensor đầu ra tổng thể (outputs): [2, 3, 2]
Kích thước Hidden State cuối cùng: [2, 2]
```