Wordcloud
Để tạo “đám mây từ” (word cloud), một hình ảnh hiển thị tần suất xuất hiện của các từ trong một đoạn văn bản. Các từ xuất hiện càng nhiều thì được vẽ càng to và đậm màu hơn, giúp bạn nhìn nhanh từ khóa quan trọng trong văn bản, bình luận, tin tức, dữ liệu chatbot,…
Cú pháp:
text = " ".join((self.df["text"]).astype(str))
wordcloud = WordCloud(width=800, height=400, background_color="white").generate(text)
