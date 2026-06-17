- [Console (đối tượng chính trong thư viện rich)](#console-đối-tượng-chính-trong-thư-viện-rich)
- [Panel (Tạo khung đẹp trong terminal)](#panel-tạo-khung-đẹp-trong-terminal)
  - [.fit() (tạo panel có kích thước vừa đủ với nội dung)](#fit-tạo-panel-có-kích-thước-vừa-đủ-với-nội-dung)
- [Progress (Class tạo thanh tiến trình)](#progress-class-tạo-thanh-tiến-trình)
  - [add\_task() (dùng để tạo một công việc (task) cho Progress theo dõi)](#add_task-dùng-để-tạo-một-công-việc-task-cho-progress-theo-dõi)
- [SpinnerColumn() (Thêm cột spinner (quay vòng loading))](#spinnercolumn-thêm-cột-spinner-quay-vòng-loading)
- [TextColumn() (Hiển thị text bên cạnh spinner)](#textcolumn-hiển-thị-text-bên-cạnh-spinner)
---
# Console (đối tượng chính trong thư viện rich)
```bash
Có thể dùng để:
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
## .fit() (tạo panel có kích thước vừa đủ với nội dung)
```bash
- Trong Rich có class Panel. Thông thường: Panel("Hello")
    + Panel sẽ cố gắng chiếm toàn bộ chiều ngang terminal.
    ┌───────────────────────────────────────┐
    │ Hello                                 │
    └───────────────────────────────────────┘
- Panel.fit().
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
# Progress (Class tạo thanh tiến trình)
**Syn**
```bash
Progress(
    ...
    transient=True
)

- transient=True: Sau khi hoàn thành thì xóa progress khỏi terminal
```
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
## add_task() (dùng để tạo một công việc (task) cho Progress theo dõi)
```bash
Bạn có thể hiểu đơn giản:
    - Progress = bảng theo dõi tiến độ
    - Task = một công việc cụ thể trong bảng đó
```
**Ex**
```python
from rich.progress import Progress
import time

with Progress() as progress:
    task = progress.add_task(
        "Đang tải dữ liệu...",
        total=100
    )

    for i in range(100):
        time.sleep(0.05)
        progress.update(task, advance=1)
# Đang tải dữ liệu... ━━━━━━━━━━━━━━━━━━━━━━━━ 100%
```
# SpinnerColumn() (Thêm cột spinner (quay vòng loading))
```bash
SpinnerColumn() chỉ có nhiệm vụ hiển thị biểu tượng loading đang quay trên terminal.
```
**Ex**
```python
import time
from rich.progress import Progress, SpinnerColumn, TextColumn

with Progress(
    SpinnerColumn(),
    TextColumn("{task.description}")
) as progress:

    progress.add_task(
        description="Đang xử lý dữ liệu..."
    )

    time.sleep(5)

# Khi chương trình đang chạy
# Spinner sẽ quay liên tục:
# ⠋ Đang xử lý dữ liệu... sau khoảng 0.1 giây:
# ⠙ Đang xử lý dữ liệu... sau đó:
# ⠹ Đang xử lý dữ liệu... rồi:
# ⠸ Đang xử lý dữ liệu... rồi:
# ⠼ Đang xử lý dữ liệu...
# ...
# Người dùng nhìn thấy:
# ⠋ Đang xử lý dữ liệu...
# ⠙ Đang xử lý dữ liệu...
# ⠹ Đang xử lý dữ liệu...
# ⠸ Đang xử lý dữ liệu...
# ⠼ Đang xử lý dữ liệu...
# ...
# nhưng thực tế Rich liên tục ghi đè lên cùng một dòng nên bạn sẽ thấy nó như một biểu tượng đang quay.
```
# TextColumn() (Hiển thị text bên cạnh spinner)