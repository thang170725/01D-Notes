# .findall()
```bash
Lấy tất cả các chuỗi khớp. Rất hay dùng để: Crawl dữ liệu, Parse log. Trích số / email / URL.
```
**Ex**
```python
text = "Các số: 10, 20 và 30"
nums = re.findall(r"\d+", text)
print(nums)   # ['10', '20', '30']
```