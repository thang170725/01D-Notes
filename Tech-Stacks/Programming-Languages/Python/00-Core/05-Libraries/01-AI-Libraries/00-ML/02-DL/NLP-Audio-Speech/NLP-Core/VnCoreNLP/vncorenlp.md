VnCoreNLP
VnCoreNLP chạy bằng Java + Python wrapper, nên bạn cần: pip install vncorenlp
Download()
from vncorenlp import VnCoreNLP

# Tự động tải file VnCoreNLP-1.1.1.jar và models
VnCoreNLP.download('VnCoreNLP-1.1.1.jar', save_dir='./')
VnCoreNLP()
from vncorenlp import VnCoreNLP

# Khởi tạo annotator: chỉ dùng word segmentation (wseg)
annotator = VnCoreNLP(
    address="http://127.0.0.1",
    port=9000,
    annotators="wseg",
    max_heap_size='-Xmx2g'  # 2GB RAM
)

text = "Tôi đang học xử lý ngôn ngữ tự nhiên tiếng Việt và muốn tách từ."

result = annotator.annotate(text)

print(result["sentences"][0])
['Tôi', 'đang', 'học', 'xử_lý', 'ngôn_ngữ_tự_nhiên', 'tiếng_Việt', 'và', 'muốn', 'tách', 'từ', '.']
