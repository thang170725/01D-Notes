# Sentence Transformer Introduction
# Installation
```bash
1. pip install sentence-transformers
```
from sentence_transformers import SentenceTransformer
from sklearn.metrics.pairwise import cosine_similarity

# Load model
model = SentenceTransformer("all-MiniLM-L6-v2")

# Các câu
sentences = [
    "Tôi thích học trí tuệ nhân tạo.",
    "Tôi rất yêu AI.",
    "Hôm nay trời mưa."
]

# Sinh embedding
embeddings = model.encode(sentences)

# So sánh độ giống nhau
similarity = cosine_similarity(embeddings)

print(similarity)
(.venv) PS D:\workspace\test> python test.py
Warning: You are sending unauthenticated requests to the HF Hub. Please set a HF_TOKEN to enable higher rate limits and faster downloads.
modules.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 349/349 [00:00<?, ?B/s]
D:\workspace\test\.venv\Lib\site-packages\huggingface_hub\file_download.py:139: UserWarning: `huggingface_hub` cache-system uses symlinks by default to efficiently store duplicated files but your machine does not support them in C:\Users\thang.ld\.cache\huggingface\hub\models--sentence-transformers--all-MiniLM-L6-v2. Caching files will still work but in a degraded version that might require more space on your disk. This warning can be disabled by setting the `HF_HUB_DISABLE_SYMLINKS_WARNING` environment variable. For more details, see https://huggingface.co/docs/huggingface_hub/how-to-cache#limitations.
To support symlinks on Windows, you either need to activate Developer Mode or to run Python as an administrator. In order to activate developer mode, see this article: https://docs.microsoft.com/en-us/windows/apps/get-started/enable-your-device-for-development
  warnings.warn(message)
config_sentence_transformers.json: 100%|█████████████████████████████████████████████████████████████████████████████████████████████| 116/116 [00:00<?, ?B/s]
README.md: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████| 10.5k/10.5k [00:00<00:00, 10.2MB/s]
sentence_bert_config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 53.0/53.0 [00:00<?, ?B/s]
config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 612/612 [00:00<?, ?B/s]
model.safetensors: downloading bytes: ████████████████████████████████████████████████████████████████████████████████████████████████████| 85.0MB, 2.25MB/s  
model.safetensors: reconstructing file: 100%|████████████████████████████████████████████████████████████████████████████████████| 90.9MB / 90.9MB, 3.50MB/s  
Loading weights: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 103/103 [00:00<00:00, 2973.48it/s]
tokenizer_config.json: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████| 350/350 [00:00<?, ?B/s]
vocab.txt: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 232k/232k [00:00<00:00, 621kB/s]
tokenizer.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 466k/466k [00:00<00:00, 1.55MB/s]
special_tokens_map.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████| 112/112 [00:00<?, ?B/s]
config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 190/190 [00:00<?, ?B/s]
[[1.        0.5026742 0.4886267]
 [0.5026742 0.9999998 0.5070527]
 [0.4886267 0.5070527 0.9999999]]
(.venv) PS D:\workspace\test> 
