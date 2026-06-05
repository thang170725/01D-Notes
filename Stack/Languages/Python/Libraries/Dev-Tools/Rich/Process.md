- [Console](#console)
- [Panel (Tạo khung đẹp trong terminal)](#panel-tạo-khung-đẹp-trong-terminal)
  - [.fit()](#fit)
- [Progress (Tạo progress bar)](#progress-tạo-progress-bar)
---
# Console 
```bash
- Đây là đối tượng chính trong thư viện rich.
- Có thể dùng để:
    + in màu
    + log
    + progress bar
    + panel
    + markdown
    + tree
```
# Panel (Tạo khung đẹp trong terminal)
```python
from rich.panel import Panel
from rich.console import Console

console = Console()

console.print(
    Panel("Convert thành công")
)
# ┌─────────────────────┐
# │ Convert thành công  │
# └─────────────────────┘
```
**Ex2: hiển thị có tiêu đề**
```python
console.print(
    Panel(
        "SVG → PDF",
        title="Thông báo"
    )
)
```
## .fit() 
```bash
- Trong Rich có class Panel. Thông thường: Panel("Hello")
    + Panel sẽ cố gắng chiếm toàn bộ chiều ngang terminal.
    ┌───────────────────────────────────────┐
    │ Hello                                 │
    └───────────────────────────────────────┘
- Panel.fit() tạo panel có kích thước vừa đủ với nội dung.
    + Panel.fit("Hello")
    ┌───────┐
    │ Hello │
    └───────┘
```
**Syn**
```bash
Panel.fit(
    renderable,
    title=None,
    subtitle=None,
    border_style=None,
    ...
)
```
# Progress (Tạo progress bar)
```python
import time
from rich.progress import Progress

with Progress() as progress:
    task = progress.add_task(
        "Đang xử lý...",
        total=100
    )

    while not progress.finished:
        progress.update(
            task,
            advance=1
        )
        time.sleep(0.05)
```