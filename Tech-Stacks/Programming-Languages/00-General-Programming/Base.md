- [General Programming Introduction (kiến thức lập trình chung)](#general-programming-introduction-kiến-thức-lập-trình-chung)
- [Ask](#ask)
  - [khi nào nên dùng OOP, khi nào nên dùng module?](#khi-nào-nên-dùng-oop-khi-nào-nên-dùng-module)
---
# General Programming Introduction (kiến thức lập trình chung)
```bash
Đây là chứa các kiến thức lập trình mà ngôn ngữ nào cũng có.
```
# Ask
## khi nào nên dùng OOP, khi nào nên dùng module?
```bash
thực tế:
    - Module -> là cách tổ chức code
    - OOP -> là cách mô hình hóa logic bằng object
-> Hai cái này có thể dùng cùng nhau.
```
**Ex**
```bash
app/
│
├── core/
│   ├── loader.py
│   ├── saver.py
│   └── trainer.py
│
├── pipelines/
│   ├── train_pipeline.py
│   └── inference_pipeline.py
│
└── main.py
-> hoàn toàn có thể là một project chuyên nghiệp.

Và bạn có thể có:
app/
│
├── core/
│   ├── model.py       ← OOP
│   ├── trainer.py     ← function
│   ├── loader.py      ← function
│   └── saver.py       ← function
│
├── pipelines/
│   └── train_pipeline.py
│
└── main.py
-> Đây mới là tư duy đúng: Chỗ nào OOP có lợi thì dùng OOP. Chỗ nào function/module phù hợp thì dùng function/module.
```
**OOP thực sự giải quyết vấn đề gì?**
```bash
OOP hữu ích khi một "thứ" có state + behavior + identity và bạn cần quản lý chúng cùng nhau.

Ví dụ rất rõ trong AI:
    model = YOLO(...)
        Model này có:
            state
            ├── weights
            ├── model architecture
            ├── device
            ├── hyperparameters
            ├── training state
            └── configuration

            behavior
            ├── train()
            ├── predict()
            ├── validate()
            ├── save()
            └── load()
-> Đây là một object rất tự nhiên.
```
**Một ví dụ để bạn thấy sự khác biệt**
```bash
Giả sử bạn có:
    - def load_csv(path):
    - def load_json(path):
    - def load_image(path):

Tôi không thấy lý do gì phải viết:
    class Loader:
        def load_csv(self, path):
        def load_json(self, path):
        def load_image(self, path):

Rồi dùng:
    loader = Loader()
    loader.load_csv(...)
    loader.load_json(...)

Trong trường hợp này:
    load_csv(path) -> đơn giản và rõ ràng hơn: Loader().load_csv(path)

-> Class Loader ở đây gần như chỉ là cái hộp để nhét các function vào. Đó thường là dấu hiệu OOP đang bị lạm dụng.
```