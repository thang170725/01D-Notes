- [Introduction](#introduction)
- [Installation](#installation)
- [có thanh tiến trình xuất hiện và tăng lên sau mỗi 0.5s](#có-thanh-tiến-trình-xuất-hiện-và-tăng-lên-sau-mỗi-05s)
---
# Directory Structure
```bash
TQDM/
├── 01_basic_iterator.md      # Cơ bản: tqdm(range), tqdm(list), desc, unit
├── 02_integration_pandas.md  # Tích hợp: progress_apply cho Series/DataFrame
├── 03_manual_control.md      # Thủ công: pbar.update(), n_total (dùng cho download/stream)
├── 04_environments.md        # Môi trường: tqdm.notebook (cho Jupyter), trange, color
└── 05_advanced_parallel.md   # Nâng cao: Dùng chung với Multiprocessing, Threading
```
# Introduction
```bash
Để tạo thanh tiến trình, thường dùng khi có vòng lặp chạy lâu.
```
# Installation
```bash
pip install tqdm
```
