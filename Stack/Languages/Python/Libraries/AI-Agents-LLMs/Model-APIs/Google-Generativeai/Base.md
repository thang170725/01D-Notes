Google-generativeai
pip install google-generativeai hoặc pip install --upgrade google-generativeai (nếu lỗi trước đó).
cần import google.generativeai as genai
Configure()

Bài tập
Kiểm tra xem API key có model gì 
import google.generativeai as genai

genai.configure(api_key="YOUR_KEY")

for m in genai.list_models():
    print(m.name, m.supported_generation_methods)
Demo nhanh
import google.generativeai as genai

genai.configure(api_key="YOUR_KEY")
model = genai.GenerativeModel("gemini-2.5-flash")
prompt = "Toán rời rạc học những gì? Trả lời dưới 100 chữ."
response = model.generate_content(prompt)

print(response.text)
