- [with\_structured\_output (đúng chính tả là structured, không phải structure) dùng để ép model trả về kết quả theo một cấu trúc cố định (schema) thay vì trả về text tự do.](#with_structured_output-đúng-chính-tả-là-structured-không-phải-structure-dùng-để-ép-model-trả-về-kết-quả-theo-một-cấu-trúc-cố-định-schema-thay-vì-trả-về-text-tự-do)
---
# with_structured_output()
```bash
- dùng để ép model trả về kết quả theo một cấu trúc cố định (schema) thay vì trả về text tự do.
- Nó rất hữu ích khi bạn muốn:
    + Nhận JSON đúng format
    + Parse dữ liệu an toàn
    + Tránh lỗi model trả lời lung tung
    + Dùng cho API backend / automation
```
**Ex**
```python
from pydantic import BaseModel

class Person(BaseModel):
    name: str
    age: int

structured_llm = llm.with_structured_output(Person)

result = structured_llm.invoke("Nam 25 tuổi")
print(result)

# Kết quả luôn là object:
# Person(name='Nam', age=25)
```