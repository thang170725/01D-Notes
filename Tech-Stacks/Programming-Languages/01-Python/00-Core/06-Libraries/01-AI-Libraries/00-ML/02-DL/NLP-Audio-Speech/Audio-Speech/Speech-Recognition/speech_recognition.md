speech_recognition
Để chuyển giọng nói thành văn bản.
pip install SpeechRecognition, nếu dùng micro thì nên cài thêm pyaudio, pip install pyaudio
Recognizer()
Tạo một đối tượng nhận diện bằng giọng nói.
Microphone()
Lấy dữ liệu âm thanh từ micro.
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.Microphone() as source:
    print("Nói gì đi...")
    audio = r.listen(source)
AudioFile()
Mở file âm thanh (wav, aif, flac).
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.AudioFile('test.wav') as source:
    audio = r.record(source)
.listen()
Ghi lại âm thanh từ nguồn micro.
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.Microphone() as source:
    print("Đang ghi âm...")
    audio = r.listen(source)
    print("Xong!")
Record()
Ghi âm trong N giây.
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.AudioFile('test.wav') as source:
     audio = r.record(source, duration=5)  # Lấy 5 giây đầu
adjust_for_ambient_noise()
Chống nhiễu.
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.Microphone() as source:
    r.adjust_for_ambient_noise(source, duration=1)
    print("Bắt đầu nói...")
    audio = r.listen(source)
recognize_google()
Nhận diện bằng giọng nói google. Cái này thường để in ra nội dung nói
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.AudioFile('test.wav') as source:
    audio = r.record(source)

text = r.recognize_google(audio, language='vi-VN')
print("Nội dung:", text)
UnknownValueError và Requesterror
Cú pháp:
import speech_recognition as sr

r = sr.Recognizer()
with sr.Microphone() as source:
    print("Nói đi...")
    audio = r.listen(source)

try:
    text = r.recognize_google(audio)
    print("Bạn nói:", text)
except sr.UnknownValueError:
    print("Không hiểu bạn nói gì.")
except sr.RequestError:
    print("Không kết nối được tới Google.")
