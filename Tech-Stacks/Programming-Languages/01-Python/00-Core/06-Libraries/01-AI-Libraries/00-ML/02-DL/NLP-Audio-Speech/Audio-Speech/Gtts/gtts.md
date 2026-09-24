GTTS
Chuyển văn ban thành giọng nói. Cần có internet.
pip install gTTS, cần from gtts import gTTS
Cú pháp:
gTTS(text, lang='en', slow=False, tld='com')
    • text: Văn bản cần chuyền giọng nói.
    • lang: Mã ngôn ngữ
    • slow: True là đọc chậm, False là đọc bình thường.
    • tld: Miền Google – Thay đổi chất giọng.
import speech_recognition as sr
from gtts import gTTS
import os
import time # chờ file trước khi xóa
r = sr.Recognizer()
with sr.Microphone() as source:
    r.adjust_for_ambient_noise(source, duration=2)
    print("bạn hãy nói gì đó và tôi sẽ nhắc lại câu bạn vừa nói ...")
    audio = r.listen(source)
try:
    text = r.recognize_google(audio, language='vi-VN')
    print("bạn đã nói: ", text)
    # chuyện thành lời thoại
    tts = gTTS(text=text, lang='vi', slow=False, tld='com')
    fileName = "output.mp3"
    # lưu file âm thanh
    tts.save(fileName)
    os.system(f"start {fileName}")
    # chờ một chút trước khi xóa để file chạy xong
    time.sleep(20)
    os.remove(fileName)
except sr.UnknownValueError:
    print("error")
except sr.RequestError:
    print("không thể kết nối với Google")
