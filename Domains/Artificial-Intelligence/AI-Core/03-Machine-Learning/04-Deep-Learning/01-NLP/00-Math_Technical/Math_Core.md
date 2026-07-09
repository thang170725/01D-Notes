# Gradient
## BPTT (Backpropagation Through Time)
    • Đây là kỹ thuật tính gradient cho RNN. Vì RNN có trạng thái ẩn h_t phụ thuộc vào tất cả các h_(t-1), h_(t-2), …, nên backprop bình thường không đủ, ta phải "trải graph ra theo thời gian" và tính gradient qua từng step.
    • Về cơ bản: BPTT là backpropagation chuẩn, nhưng áp dụng lên graph được unfold theo time steps.
    • Công thức: dL/dW = sum((dL/dh_t) . (dh_t/dW))
Cú pháp:
# Forward RNN qua seq_len steps
h = torch.zeros(batch, hidden_dim)
for t in range(seq_len):
    h = torch.tanh(X[:, t, :] @ Wxh + h @ Whh + bh)

# Loss dựa trên h cuối
loss = cross_entropy(h @ Why + by, y)

# BPTT
loss.backward()  # PyTorch tự lan truyền qua tất cả h_t
### Practice
#### Demo BPTT
```python
import torch

# fake data
X = torch.tensor([[1.0, 2.0, 3.0]], requires_grad=False) # batch=1, input_dim=3
y_true = torch.tensor([0]) # label

# RNN params
Wxh = torch.randn(3, 3, requires_grad=True) # (input_dim, hidden_dim)
Whh = torch.randn(3, 3, requires_grad=True) # (hidden_dim, hidden_dim)
Why = torch.randn(3, 2, requires_grad=True) # (hidden_dim, output_dim)
bh = torch.zeros(3, requires_grad=True)
by = torch.zeros(2, requires_grad=True)

h_t = torch.zeros(1, 3)
lr = 0.01
seq_len = 2

for i in range(seq_len): # giả sử có h_0, h_1
    # forward RNN
    h_t = torch.tanh(X@Wxh + h_t@Whh + bh)

# compute loss từ h cuối
logits = h_t@Why + by
loss = torch.nn.CrossEntropyLoss()(logits, y_true)
cross_entropy = torch.nn.CrossEntropyLoss()

# BPTT: backward toàn bộ sequence
loss.backward()

# SGD update
with torch.no_grad():
    for p in [Wxh, Whh, Why, bh, by]:
        p -= lr*p.grad
        p.grad.zero_()
    
print(f'Updated params', Wxh, Whh, Why, bh, by)
```