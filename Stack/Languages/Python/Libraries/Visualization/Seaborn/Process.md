Seaborn
Là một thư viện vẽ biểu đồ mạnh mẽ trong Python, được xây dựng trên nền tảng Matplotlib, và tích hợp rất tốt với Pandas. Kế thừa matplotlib
pip install seaborn
So sánh seaborn và matplotlib:

Matplotlib
Seaborn
Cấp độ
Thấp (Low-level)
Cao (High-level, built on Matplotlib)
Cú pháp
Tự kiểm soát từng chi tiết (trục, màu, tick...)
Dễ viết, đẹp sẵn, hiểu dữ liệu dạng bảng
Dữ liệu truyền vào
Mảng, list, numpy...
DataFrame (pandas) là chính
Biểu đồ phù hợp
Biểu đồ cơ bản, tùy biến sâu (line, scatter, bar, hist...)
Biểu đồ thống kê, phân tích quan hệ (countplot, boxplot, pairplot, heatmap…)
Tốc độ viết code
Nhiều dòng hơn, linh hoạt hơn
Ngắn gọn, tự động nhận dạng biến
Phong cách mặc định
Khá “thô” nếu không chỉnh
Mặc định rất đẹp và hiện đại
Countplot()
Cú pháp:
sns.countplot(x='intent', data=self.df, palette='Set2', ax=ax)

Violinplot()
Lmplot()
Histplot()
Boxplot()
 sns.boxplot(x="intent", y="length", data=self.df, ax=ax)

Scatterplot()
Lineplot()
Heatmap()
Pairplot()
Barplot()

