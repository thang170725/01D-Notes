Mysqlconnector
Launch()
Khởi động trình duyệt (Chromium, Firefox, WebKit).
Cú pháp:
browser = playwright.chromium.launch(headless=False)
new_context()
Tạo một "phiên" làm việc riêng biệt (giống như cửa sổ ẩn danh), không chia sẻ cookie/cache.

context = browser.new_context()

new_page()
Mở một tab mới trong trình duyệt.

page = context.new_page()
.goto()
.get_by_role()
.get_by_text()
.locator()
.get_by_placeholder()
.fill
.click()
inner_text	Lấy nội dung văn bản bên trong một thẻ.	content = page.locator("h1").inner_text()
get_attribute	Lấy giá trị thuộc tính (ví dụ link href, nguồn ảnh src).	link = page.locator("a").get_attribute("href")
expect	(Chế độ Test) Kiểm tra một điều kiện có đúng hay không.	expect(page).to_have_title("Dashboard")6. Hack

Mã cổ điển
Quy định sử dụng mã cổ điển:
    • Thuật toán mã hóa mạnh.
    • Khóa mật chỉ có người gửi và người nhận biết.
Ưu điểm
Nhược điểm
    • Đơn giản
    • Dễ bị phá giải mã bằng cách đoán chữ.
    • Hai bên mã hóa và giải mã phải thống nhất với nhau về cơ chế mã hóa cũng như giải mã.
Hệ mã Vigenere
Sử dụng khóa có độ dài m. Nó bao gồm m phép mã hóa bằng dịch chuyển được áp dụng luân phiên nhau theo chu kỳ.
Không gian khóa K của phương pháp có số phần tử .
Ví dụ
Ý tưởng:
    1. Lặp lại từ khóa sao cho bằng thông điệp. (khóa là apple, thông điệp là iamastudent).
→ khóa là appleapplea.
    2. Tạo bảng từ 0 – 25 lưu các giá trị a – z. (0:a, 1:b, …)
    3. Lần lượt lấy các chữ của thông điệp cộng với các chữ cái của khóa. (i(8) + a(0) = 8)
    4. Chuyển số thành chữ ở bước 3 ( 8 = p). nếu phần tử lớn quá 25 thì phải mod với 26.
    5. Lặp lại bước 3 và bước 4 sao cho khi lặp hết qua thông điệp thì dừng lại.
Code:
import string
class Vigenere:
    def tableDic(self):
        dic = {index: value for index, value in enumerate(string.ascii_lowercase)}
        return dic
    def encodeVigenere(self, str, key):
        # tạo biến kết quả của quá trình mã hóa
        result = ""
        # lặp lại từ khóa cho đến khi nó có độ dài bằng với chuỗi
        if len(str) >= len(key):
            if len(str) > len(key):
                for i in range(len(str) - len(key)):
                    key += key[i % len(key)]
                for i in range(len(str)):
                    # chuyển chữ thành số
                    x = (ord(str[i]) - ord("a") + ord(key[i]) - ord("a")) % 26
                    # chuyển số thành chữ
                    result += self.tableDic()[x]
                return result
            else:
                return "key is not longer than input string"

Hệ mã Affine
Không gian các bản rõ và các bản mã là các xâu được hình thành từ một bảng chữ cái A.
Ví dụ
Giả sử chúng ta muốn mã hóa từ "HELLO" bằng hệ mã Affine với khóa a = 5 và b = 8.
Ý tưởng:
    1. Chuyển đổi chữ cái thành số (H = 7, E = 4, L = 11, …)
    2. Áp dụng công thức (a*char[i] + b) mod 26
    • E(7) = (5 * 7 + 8) mod 26 = 43 mod 26 = 17 = R
    • E(4) = (5 * 4 + 8) mod 26 = 28 mod 26 = 2 = C
    • E(11) = (5 * 11 + 8) mod 26 = 63 mod 26 = 11 = L
    • E(11) = (5 * 11 + 8) mod 26 = 63 mod 26 = 11 = L
    • E(14) = (5 * 14 + 8) mod 26 = 78 mod 26 = 0 = A
Vậy, từ "HELLO" sau khi mã hóa chính xác là "RCLLA".
Code:
Output: rclla
class Affine:
    def tableDic(self):
        return {index: value for index, value in enumerate(string.ascii_lowercase)}
    def encodeAffine(self, str, k1, k2):
        # element save result of Affine
        result = ""
        for i in range(len(str)):
            # change character in str to number
            x = ord(str[i]) - ord("a")
            # apply Affine mathematical calculation
            n = (k1*x + k2) % 26
            # change number to character
            result = result + self.tableDic()[n]
        return result
def main():
    affine = Affine()
    print(affine.encodeAffine("hello", 5, 8))
main()

Hệ mã Hill
Nó sử dụng đại số tuyến tính để mã hóa văn bản, biến mỗi khối ký tự thành một khối ký tự khác thông qua phép nhân ma trận.
Nguyên tắc hoạt động:
    1. Chuyển đổi ký tự thành số: Mỗi ký tự trong bảng chữ cái được gán một giá trị số tương ứng (A=0, B=1, …).
    2. Phân chia văn bản: Văn bản gốc được chia thành các khối ký tự có độ dài bằng kích thước của ma trận khóa.
    3. Mã hóa:
        a. Mỗi khối ký tự được biểu diễn dưới dạng một vector cột.
        b. Vector cột này được nhân với một ma trận khóa.
        c. Kết quẩ của phép nhân ma trận được lấy modulo 26.
        d. Chuyển đổi số thành chữ.
Giải mã:
    • Để giải mã, người nhận cần biết ma trận khóa. 
    • Người nhận thực hiện các bước tương tự như mã hóa, nhưng thay vì nhân với ma trận khóa, họ nhân với ma trận nghịch đảo của ma trận khóa.
Ví dụ
Giả sử chúng ta muốn mã hóa từ "CAT" với ma trận khóa sau: 
Ý tưởng:
[ 6  24  1]
[ 13 16 10]
[ 20 17 15]
Chuyển đổi ký tự thành số: 
C = 2, A = 0, T = 19
Biểu diễn dưới dạng vectơ cột:
[ 2 ]
[ 0 ]
[ 19]
Mã hóa: 
Nhân vectơ cột với ma trận khóa và lấy modulo 26:
[ 6  24  1]   [ 2 ]   [ 482 ]   [ 14 ]
[ 13 16 10] x [ 0 ] = [ 190 ] = [ 8 ]
[ 20 17 15]   [ 19]   [ 685 ]   [ 9]
Chuyển đổi số thành ký tự: 
4 = E, 8 = I, 15 = P
Vậy, "CAT" được mã hóa thành "EIP".
Lưu ý:
Ma trận khóa phải khả nghịch (có ma trận nghịch đảo) để có thể giải mã.
Hệ mã Hill dễ bị tấn công nếu biết một số lượng đủ lớn các cặp văn bản gốc và văn bản mã hóa.
Các phép tính được thực hiện trên vành Z26.
Hệ mã Hill là một ví dụ thú vị về việc sử dụng đại số tuyến tính trong mật mã học. Mặc dù nó không còn được sử dụng rộng rãi trong các ứng dụng bảo mật hiện đại, nhưng nó vẫn là một khái niệm quan trọng trong lịch sử mật mã.
Hệ mã Playfair
Là một kĩ thuật mã hóa chữ đôi
Nguyên lý hoạt động: Sử dụng bảng chữ cái 5x5 để mã hóa các cặp chữ cái
    • Bảng chứa 25 chữ cái (chữ I và j thường đưcọ gộp lại làm một).
    • Người dùng chọn một từ khóa để tạo bản mã này.
Ví dụ
Mã hóa từ “hello” bằng với từ khóa “monarchy”.
Ý tưởng:
    1. Tạo bảng khóa
    • Bảng chữ cái: A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    • Đã dùng rồi: M O N A R C H Y
    • Chưa dùng: B, D, E, F, G, I/J, K, L, P, Q, S, T, U, V, W, X, Z
M O N A R  
C H Y B D  
E F G I/J K  
L P Q S T  
U V W X Z  
    2. Tạo cặp của dữ liệu: (he, lx, lo) Nếu có 2 chữ cái giống nhau trong 1 cặp, chèn một chữ X giữa. Nếu tổng số chữ là lẻ, thêm X vào cuối.
    3. Mã hóa:
Chữ H ở hàng 2, cột 2
Chữ E ở hàng 3, cột 1
→ Chúng ta tạo hình chữ nhật → Thay H bằng chữ ở hàng 2, cột 1 → C
→ Thay E bằng chữ ở hàng 3, cột 2 → F
→ HE → CF
→ Tương tự ta có LX → SU, LO → MP
    4. Kết quả: hello → cfsump
Hệ mã transposition cipher
Là một dạng mã hóa cổ điển, trong đó thứ tự các ký tự trong bản rõ bị thay đổi theo một quy tắc nhất định, nhưng bản thân ký tự không bị thay đổi.
Nguyên lý hoạt động:
    • Không thay đổi ký tự, chỉ thay đổi vị trí.
    • Người gửi và người nhận phải biết quy tắc đổi chỗ
    • Nếu không có khóa việc giải mã rất khó.
Ví dụ
Mã hóa “hello world” bằng khóa cột “3142”
    1. Loại bỏ khoảng trắng
    2. Tạo bảng hàng cột:
H  E  L  L  
O  W  O  R  
L  D  _  _  (dùng dấu gạch dưới để điền thêm cho đủ hàng)
    3. Sắp xếp:
Cột 3: l, o
Cột 1: h, o, l
…
    4. Kết quả: lohollrewd
Mã hoán vị
Hệ mã Rail Frence
Là một kĩ thuật mã hóa đơn giản, hoán vị các chữ cái, không thay thế chúng.
Ví dụ
Mã hóa “we are discovered run at once” với đường ray (rails) là 3
Ý tưởng:
    1. Bỏ qua khoảng trắng: wearediscoveredrunatone
    2. Viết theo kiểu zigzag:
Rail 1: W -  -  - E  -  -  - C -  -  - R -  - - U -  - - O
Rail 2:  -  E -  R - D  -  S - O - E - E - R - N - T - N
Rail 3:  -  -  A  - - -   I   -  - - V - - -  D -  -  - A - -  - E 
    3. Ghi lại các chữ cái theo đường ray từ trên xuống
Rail1: wecruo
Rail2: erdsoeerntn
Rail3: aivdae
    4. Kết quả: wecruoerdsoeerntnaivdae
Chuẩn hóa dữ liệu DES (Data Encryption Standard)
Là một thuật toán mã hóa khối đối xứng. Điều này có nghĩa là nó sử dụng cùng một khóa cho cả quá trình mã hóa và giải mã. DES hoạt động trên các khối dữ liệu 64 bit và sử dụng khóa 56 bit.
Giải thích dễ hiểu:
Hãy tưởng tượng bạn có một hộp khóa bí mật (khóa 56 bit) và một tin nhắn (khối dữ liệu 64 bit). DES giống như một quy trình phức tạp để xáo trộn tin nhắn của bạn bằng hộp khóa đó, biến nó thành một mớ hỗn độn không thể đọc được (văn bản mã hóa). Chỉ những người có hộp khóa giống hệt mới có thể đảo ngược quá trình và khôi phục tin nhắn gốc.
Ví dụ
Giả sử bạn muốn gửi tin nhắn "HELLO" bằng DES.
    1. Chuyển đổi: Tin nhắn "HELLO" được chuyển đổi thành một chuỗi bit 64 bit.
    2. Mã hóa: DES sử dụng khóa 56 bit của bạn để xáo trộn chuỗi bit này qua một loạt các phép biến đổi phức tạp.
    3. Văn bản mã hóa: Kết quả là một chuỗi bit 64 bit khác, trông giống như một mớ dữ liệu ngẫu nhiên.
    4. Giải mã: Người nhận có khóa 56 bit giống hệt có thể sử dụng DES để đảo ngược quá trình và khôi phục chuỗi bit "HELLO" ban đầu.
Thuật toán DES
DES hoạt động theo một quy trình gồm 16 vòng lặp, mỗi vòng lặp bao gồm các bước sau:
    1. Hoán vị ban đầu (IP): Các bit của khối dữ liệu được xáo trộn theo một cách cố định.
    2. Phân chia: Khối dữ liệu được chia thành hai nửa, mỗi nửa 32 bit.
    3. Hàm F: Nửa phải của dữ liệu và một khóa con (được tạo từ khóa 56 bit chính) được đưa vào một hàm phức tạp. Hàm F bao gồm các phép hoán vị, thay thế và XOR.
    4. Hoán vị P: Đầu ra của hàm F được hoán vị.
    5. XOR: Đầu ra của hoán vị P được XOR với nửa trái của dữ liệu.
    6. Hoán đổi: Nửa trái và nửa phải của dữ liệu được hoán đổi.
    7. Hoán vị cuối cùng (IP^-1): Các bit của khối dữ liệu được xáo trộn theo cách đảo ngược của hoán vị ban đầu.
Điểm yếu của DES:
    • Kích thước khóa nhỏ: Khóa 56 bit của DES được coi là quá nhỏ theo tiêu chuẩn hiện đại, khiến nó dễ bị tấn công vét cạn (brute-force attack).
    • Thiết kế gây tranh cãi: Có những lo ngại rằng thiết kế của DES có thể chứa các cửa hậu (backdoor) cho phép các cơ quan chính phủ giải mã dữ liệu.
Sự thay thế:
Do những điểm yếu này, DES đã được thay thế bằng các thuật toán mã hóa mạnh hơn như AES (Advanced Encryption Standard).
Tóm lại:
DES là một thuật toán mã hóa khối đối xứng đã từng rất phổ biến, nhưng hiện nay được coi là không an toàn do kích thước khóa nhỏ. Nó hoạt động bằng cách xáo trộn dữ liệu qua một loạt các phép biến đổi phức tạp, sử dụng cùng một khóa cho cả mã hóa và giải mã.
Mã hóa DES (Data Encryption Standard) là một thuật toán mã hóa khối đối xứng, hoạt động trên các khối dữ liệu 64 bit và sử dụng khóa 56 bit. Quá trình mã hóa DES bao gồm 16 vòng lặp, mỗi vòng lặp thực hiện các bước biến đổi phức tạp trên dữ liệu.
Tuy nhiên, việc mô tả chi tiết từng bước trong 16 vòng lặp với dữ liệu đầu vào "hello" là cực kỳ phức tạp và không thực tế để thực hiện thủ công. Thay vào đó, tôi sẽ cung cấp một cái nhìn tổng quan về quy trình mã hóa DES và những bước chính trong mỗi vòng lặp.
Quy trình mã hóa DES:
    1. Chuyển đổi dữ liệu đầu vào: 
        ◦ Dữ liệu đầu vào "hello" được chuyển đổi thành chuỗi bit 64 bit.
    2. Hoán vị ban đầu (IP): 
        ◦ Các bit của khối dữ liệu được xáo trộn theo một bảng hoán vị cố định.
    3. 16 vòng lặp: 
        ◦ Mỗi vòng lặp sử dụng một khóa con 48 bit, được tạo ra từ khóa 56 bit chính.
        ◦ Trong mỗi vòng lặp, dữ liệu được chia thành hai nửa, nửa trái (L) và nửa phải (R).
        ◦ Nửa phải (R) được đưa vào hàm F, hàm này thực hiện các bước biến đổi phức tạp bao gồm: 
            ▪ Mở rộng (E): Nửa phải 32 bit được mở rộng thành 48 bit.
            ▪ XOR: Kết quả mở rộng được XOR với khóa con 48 bit.
            ▪ Thay thế (S-boxes): Kết quả XOR được đưa qua 8 hộp thay thế (S-boxes) để tạo ra đầu ra 32 bit.
            ▪ Hoán vị (P): Đầu ra 32 bit được hoán vị.
        ◦ Kết quả của hàm F được XOR với nửa trái (L).
        ◦ Nửa trái (L) và nửa phải (R) được hoán đổi cho vòng lặp tiếp theo.
    4. Hoán vị cuối cùng (IP^-1): 
        ◦ Sau 16 vòng lặp, các bit của khối dữ liệu được xáo trộn theo bảng hoán vị ngược của hoán vị ban đầu.
    5. Văn bản mã hóa: 
        ◦ Kết quả là văn bản mã hóa 64 bit.
Những điểm quan trọng:
    • Hàm F: Hàm F là cốt lõi của thuật toán DES, thực hiện các phép biến đổi phi tuyến tính để tạo ra tính bảo mật.
    • Khóa con: Mỗi vòng lặp sử dụng một khóa con khác nhau, được tạo ra từ khóa chính thông qua một quy trình tạo khóa phức tạp.
    • S-boxes: Các hộp thay thế (S-boxes) là các bảng tra cứu phi tuyến tính, cung cấp tính bảo mật cho DES.
Lưu ý:
    • Việc mô tả chi tiết từng bước trong 16 vòng lặp với dữ liệu đầu vào "hello" đòi hỏi rất nhiều phép tính toán và không thể trình bày đầy đủ ở đây.
    • DES đã được thay thế bằng các thuật toán mã hóa mạnh hơn như AES do kích thước khóa nhỏ của nó.
Tôi hy vọng thông tin này giúp bạn hiểu rõ hơn về quy trình mã hóa DES.
DataLoaderNn
Bộ quản lý dữ liệu giúp: Đọc dữ liệu từng phần nhỏ (mini-batch) thay vì đọc tất cả 1 lần.. Tự động load và đưa dữ liệu vào GPU trong khi train. Làm việc linh hoạt với mọi kiểu dữ liệu (ảnh, văn bản, số liệu,...).
Cú pháp:
dataloader = DataLoader(dataset, batch_size=2, shuffle=True)
    • Shuffle=True: (xáo trộn) dữ liệu mỗi epoch để mô hình học tốt hơn
import torch
from torch.utils.data import Dataset, DataLoader
import pandas as pd
from typing import List

class RealEstateDataset(Dataset):
    def __init__(self, 
        data_frame: pd.DataFrame, 
        features: List[str],
        label: List[str]) -> None:

        self.data = data_frame

        self.X = torch.tensor(
            self.data[features].to_numpy(), 
            dtype=torch.float32
        )
        self.y = torch.tensor(
            self.data[label].to_numpy(), 
            dtype=torch.float32
        )
    
    def __len__(self) -> int:
        return len(self.data)
    
    def __getitem__(self, idx) -> tuple:
        return self.X[idx], self.y[idx]
    
if __name__ == "__main__":
    data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }

    df = pd.DataFrame(data)
    
    features = ['size', 'bedrooms', 'age']
    labels = ['price']

    dataset = RealEstateDataset(df, features, labels)
    dataloader = DataLoader(dataset, batch_size=2, shuffle=True)

    for X_batch, y_batch in dataloader:
        print("Features:", X_batch)
        print("Labels:", y_batch)
Features: tensor([[1500.,    4.,    5.],
        [ 900.,    3.,   15.]])
Labels: tensor([[350000.],
        [250000.]])
Features: tensor([[1200.,    3.,   20.],
        [ 850.,    2.,   10.]])
Labels: tensor([[300000.],
        [200000.]])
Hệ mã RSA
def miller_rabin(p, a):
    if p < 2:
        return False
    if p == 2:
        return True
    if p%2 == 0:
        return False
    k = 0
    q = p-1
    while q%2 == 0:
        q //= 2
        k += 1
    x = pow(a, q, p)
    if x == 1 or x == p-1:
        return True
    for _ in range(k-1):
        x = pow(x, 2, p)
        if x == p-1:
            return True
        if x == 1:
            return False
    return False

def nghich_dao(a, n):
    r0, r1 = n, a
    t0, t1 = 0, 1
    while r1 != 0:
        q = r0//r1
        r0, r1 = r1, r0 -q*r1
        t0, t1 = t1, t0 - q*t1
    if r0 != 1:
        return None
    else:
        return t0%n
def RSA(p, q, e):
    n = p*q
    if miller_rabin(p, 2) and miller_rabin(q, 2) and miller_rabin(e, 2):
        wn = (p - 1) * (q - 1)
        d = nghich_dao(e, wn)

        kp = {
            'e': e,
            'n': n,
        }
        ks = {
            'd': d,
            'n': n,
        }
        return kp, ks
    return None, None

def encoder(m, e, n):
    return pow(m,e, n)
def decoder(c, d, n):
    return pow(c, d, n)

def main():
    print("======= Miller RanBin =======")
    p = int(input('Số nguyên cần kiểm tra: '))
    a = int(input('Nhập vào một số nguyên tố (0 -> p): '))
    print("số đó có thể là số nguyên tố") if miller_rabin(p, a) else print("số đó có thể không phải số nguyên tố")

    print("======= RSA =======")
    p = int(input('Nhập số nguyên tố: '))
    q = int(input(('Nhập số nguyên tố: ')))
    e = int(input(f'Nhập số nguyên tố sao cho số đó là số nguyên tố cùng nhau với {(p-1)*(q-1)}: '))
    kp, ks = RSA(11, 17, 7)
    print('Các khóa của hệ mã rsa')
    print("khóa công khai: ", kp)
    print("khóa bí mật: ", ks)
    e = kp['e']
    n = kp['n']
    d = ks['d']
    m = int(input('nhập số cần để sử dụng hệ mã msa: '))
    c = encoder(m, e, n)
    print('số sau khi mã hóa là: ', c)
    print('Hệ mã rsa giải mã số đó: ', decoder(c, d, n))
main()

