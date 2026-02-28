```bash
- Thư viện decimal dùng để tính toán số thập phân với độ chính xác cao, thay thế cho float khi:
    + Không chấp nhận sai số (tài chính, kế toán, tiền tệ)
    + So sánh số thập phân chính xác
    + Cần kiểm soát cách làm tròn
```
**Ví dụ lỗi của float**
```bash
0.1 + 0.2

Kết quả: 0.30000000000000004
```
**Ex**
```python
from decimal import Decimal

a = Decimal("0.1")
b = Decimal("0.2")

print(a + b)
print(a - b)
print(a * b)
print(a / b)

# Kết quả
# 0.3
# -0.1
# 0.02
# 0.5
```
4. So sánh Decimal (CHÍNH XÁC)
Decimal("0.3") == Decimal("0.1") + Decimal("0.2")


👉 Kết quả:

True


Trong khi:

0.3 == 0.1 + 0.2


👉

False

5. Thiết lập độ chính xác (getcontext())
from decimal import Decimal, getcontext

getcontext().prec = 4   # tổng số chữ số có nghĩa

x = Decimal("1") / Decimal("7")
print(x)

Kết quả
0.1429

6. Làm tròn số (quantize) – RẤT HAY DÙNG
6.1 Làm tròn 2 chữ số thập phân
from decimal import Decimal

x = Decimal("3.14159")
y = x.quantize(Decimal("0.00"))

print(y)


👉

3.14

6.2 Các chế độ làm tròn
from decimal import Decimal, ROUND_HALF_UP, ROUND_DOWN

x = Decimal("2.675")

print(x.quantize(Decimal("0.00"), rounding=ROUND_HALF_UP))
print(x.quantize(Decimal("0.00"), rounding=ROUND_DOWN))


👉

2.68
2.67


📌 Hay dùng trong tài chính: ROUND_HALF_UP

7. Một số hàm toán học thường dùng
from decimal import Decimal

x = Decimal("9")

print(x.sqrt())
print(x.exp())
print(x.ln())

Kết quả
3
8103.083927575384007
2.1972245773362196

8. So sánh lớn – nhỏ
a = Decimal("10.5")
b = Decimal("10.50")

print(a == b)
print(a.compare(b))


👉

True
0


📌 compare() trả về:

-1 → nhỏ hơn

0 → bằng

1 → lớn hơn

9. Ví dụ thực tế: tính tiền không sai số
from decimal import Decimal

price = Decimal("19.99")
quantity = Decimal("3")

total = price * quantity
print(total)


👉

59.97


Nếu dùng float → có thể ra 59.96999999999999

10. Tóm tắt nhanh
Vấn đề	float	decimal
Sai số	❌ Có	✅ Không
Tài chính	❌	✅
Kiểm soát làm tròn	❌	✅
Tốc độ	✅ Nhanh	❌ Chậm hơn