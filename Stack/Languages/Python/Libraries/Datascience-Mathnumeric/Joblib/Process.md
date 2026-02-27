- [.dump()](#dump)
- [.load()](#load)
---
# .dump()
```bash
Để lưu mô hình
```
**Syn**
```bash
joblib.dump(object, filename)

- object → model cần lưu
- filename → tên file (thường .pkl hoặc .joblib)
```
**Ex**
```python
joblib.dump({
    "model": model,
    "scaler": scaler,
    "feature_names": feature_names
}, "pipeline.pkl")
```
# .load()
```bash
để load model
```
**Syn**
```bash
import joblib

model = joblib.load("model.pkl")
```