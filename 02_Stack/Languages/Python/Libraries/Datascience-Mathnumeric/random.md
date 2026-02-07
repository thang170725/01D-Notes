Random
    • Để tạo ra số ngẫu nhiên.
    • Cách tạo số từ min đến max: min + rand()%(max-min+1) - rand() phải chạy từ 0 đến 1
Random()
Để tạo ra một số thực từ 0 đến 1.
Cú pháp: 
r = random.random()
random = rnd.random()
print(random) # 0.10200091582889914
Seed()
Cú pháp: 
random.seed(number)
rnd.seed(1)
for i in range(3):
    random = int(20 + rnd.random()*(30 - 20 + 1))
    print(random)
# kết quả khi chạy lần 1
21
29
28
# kết quả khi chạy lần 2
21
29
28
Randint()
Để tạo ra một số ngẫu nhiên nguyên trong phạm vi từ x đến y.
Cú pháp:
random.randint(start, end) – sinh ra số ngẫu nhiên từ start đến end
Uniform()
Tạo ra số thực trong phạm vi từ x đến y.
Cú pháp:
Random.uniform(start, end) – sinh ra số ngẫu nhiên từ start đến end
