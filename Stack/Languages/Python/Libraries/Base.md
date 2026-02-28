- [Directory Structure](#directory-structure)
---
# Directory Structure
```bash
Libraries/        # mình dùng thư mục này để xem kiến thức về thư viện Python
├── Built-In/     # mình dùng thư mục này để xem các thư viện có sẵn không cần tải
├── Data-Science/ # mình dùng thư mục này để xem  bộ công cụ dành cho dân data Science
├── Html        # mình dùng thư mục này để xem kiến thức về Html      
├── Css         # mình dùng thư mục này để xem kiến thức về Css
├── Java        # mình dùng thư mục này để xem kiến thức về Java
└── Base.md         # mình dùng file này để xem kiến thức và tiện ích
```
.
├── Built-In/    # Những thứ "có sẵn" hoặc bổ trợ cực sâu cho Python
│   ├── System/                 # os, sys, shutil, subprocess, platform
│   ├── Runtime_Concurrency/    # asyncio, threading, multi-processing, time
│   ├── Data_Types_Logic/       # collections, heapq, uuid, re (Regex), abc, typing
│   └── Math_Random/            # math, random, decimal
│
├── 02_Data_Science_Base/       # "Bộ ba xe pháo mã" của dân Data
│   ├── Numpy/
│   ├── Pandas/
│   ├── Scipy/                  # Gom scipy và integrate vào đây
│   └── Joblib/                 # Lưu/Load model và song song hóa tính toán
│
├── 03_Backend_API_Stack/       # Hệ sinh thái Web & Database (Thường đi cùng nhau)
│   ├── Frameworks/             # Fastapi, Django
│   ├── Database_ORM/           # SqlAlchemy, Alembic, mysqlconnector, psycopg2
│   ├── Security_Auth/          # Jose (JWT), Passlib, Google-Auth
│   ├── Schema_Validation/      # Pydantic (Vì FastAPI dùng Pydantic cực nhiều)
│   └── Network_Client/         # requests, socket, websocket, paho (MQTT)
│
├── 04_AI_Agents_LLMs/          # Kỷ nguyên mới: LLMs và RAG
│   ├── Frameworks/             # Langchain, LangGraph
│   └── Model_APIs/             # openai, google-generativeai
│
├── 05_Machine_Learning_Deep/   # Các "ông lớn" về huấn luyện mô hình
│   ├── Frameworks/             # PyTorch, Tensorflow, Keras
│   ├── Classical_ML/           # Sklearn, XGBoost
│   └── Utilities/              # tqdm, mosec (nếu có)
│
├── 06_Computer_Vision_OCR/     # Xử lý hình ảnh và chữ viết
│   ├── Processing/             # Open-CV, PIL, imgaug
│   ├── Detection_Tracking/     # Ultralytics (YOLO), deep_sort_realtime, deepface
│   └── OCR_Specialized/        # Easyocr, Paddleocr, Tesseract, Vietocr...
│
├── 07_NLP_Audio_Speech/        # Xử lý ngôn ngữ tự nhiên và âm thanh
│   ├── NLP_Core/               # Transformers, Nltk, Vncorenlp, Tokenizers...
│   └── Audio_Speech/           # Whisper, Speech_recognition, Pydub, Pyttsx3...
│   
├── Testings/        
│  
│
└── 08_Automation_Visualization/# Đầu ra và Tự động hóa
    ├── Visualization/          # Matplotlib, Seaborn, Vispy, Wordcloud
    └── Web_Automation/         # Playwright-Stack (Dùng để crawl data/test)