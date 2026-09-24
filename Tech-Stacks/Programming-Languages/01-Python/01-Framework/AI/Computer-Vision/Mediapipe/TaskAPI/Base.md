- [Introduction](#introduction)
---
# Introduction
```bash
- Trong các project mới, người ta thường dùng Tasks + Vision vì:
    + API thống nhất
    + load model .task
    + dễ deploy production
    + giống API mobile/web
```
**Ở phiên bản mới như MediaPipe 0.10.32, workflow thường là**
```bash
model (.task)
    ↓
BaseOptions
    ↓
TaskOptions
    ↓
Task.create_from_options()
    ↓
detect()
```