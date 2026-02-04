- [Quản lý sự kiện](#quản-lý-sự-kiện)
- [Hóa Đơn bán hàng](#hóa-đơn-bán-hàng)
- [Quản lý phiếu nhập hàng](#quản-lý-phiếu-nhập-hàng)
- [Sơ đồ lớp (cầu thủ - người - câu lạc bộ)](#sơ-đồ-lớp-cầu-thủ---người---câu-lạc-bộ)
- [Bài toán căn hộ OOP](#bài-toán-căn-hộ-oop)
- [phiếu đăng lý khóa học](#phiếu-đăng-lý-khóa-học)
---
# Quản lý sự kiện
```bash
1. Tạo danh sách n phần tử (n>=5). Mỗi sự kiện là 1 dict gồm mã, tên, địa điểm, ngày, số người.
2. Viết hàm thêm chi phí nếu chưa có.
3. Tính chi phí trung bình.
4. sắp xếp theo số người tham gia.
5. tìm và in ra sự kiện có người tham gia đông nhất.
6. chương trình chính nhập -> thêm -> sắp xếp -> tìm -> in.
```
```python
def create_event():
    while True:
        n = int(input('n = '))
        if n >= 5:
            break

    return [{
            'id': input("id = "),
            'name': input("name = "),
            'address': input("address = "),
            'day': input("day = "),
            'people': int(input("people = "))
        }
        for _ in range(n)
    ]

def add_column(events: list, key="cost"):
    for row in events:
        if key not in row.keys():
            row[key] = float(input("cost = "))

def mean_cost(events: list):
    return sum(row['cost'] for row in events)/len(events)

def sort_event(events: list):
    events.sort(key=lambda row : row['people'])

def find_max(events: list):
    m = max(row['people'] for row in events)

    return [row for row in events if row['people'] == m]

def main():
    events = create_event()
    add_column(events)
    print(mean_cost(events))
    sort_event(events)
    print(events)
    print(find_max(events))
main()
```
# Hóa Đơn bán hàng
```python
from datetime import date

class Item:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price
        self.total = quantity * price

class ItemList:
    def __init__(self):
        self.items = []
        
    def input_items(self):
        n = int(input('Số mặt hàng: '))
        for _ in range(n):
            name = input('Tên hàng: ')
            qty = int(input('Số lượng: '))
            price = float(input('Đơn giá: '))

            self.items.append(Item(name, qty, price))
    
    def sum_quantity(self):
        return sum(i.quantity for i in self.items)

    def sum_price(self):
        return sum(i.price for i in self.items)

    def sum_total(self):
        return sum(i.total for i in self.items)

    def total_row(self):
        return {
            "name": "CỘNG",
            "quantity": self.sum_quantity(),
            "price": self.sum_price(),
            "total": self.sum_total()
        }
    
class Store:
    def __init__(self, name, address, phone):
        self.name = name
        self.address = address
        self.phone = phone

class Customer:
    def __init__(self):
        self.name = input('Tên khách hàng: ')
        self.address = input('Địa chỉ khách hàng: ')

class SalesInvoice:
    def __init__(self):
        self.store = Store(
            'Đức Thắng Market',
            'Phú Đa - Hoài Đức - Hà Nội',
            '0123456789'
        )

        self.customer = Customer()
        self.item_list = ItemList()
        self.item_list.input_items()

        self.date= date.today()
        self.staff = 'Lê Đức Thắng'
    
    def print_invoice(self):
        print('\nHÓA ĐƠN BÁN HÀNG')
        print("-" * 56)

        print(self.store.name)
        print('Địa chỉ: ', self.store.address)
        print('ĐT: ', self.store.phone)
        print("-" * 56)

        print('Tên khách hàng: ', self.customer.name)
        print('Địa chỉ: ', self.customer.address)
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'SL':>6} | {'Đơn giá':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.item_list.items:
            print(f"{i.name:<15} | {i.quantity:>6} | {i.price:>12.2f} | {i.total:>15.2f}")

        print("-"*40)
        print("Tổng tiền:", self.item_list.sum_total())
        print(self.date, "|", self.staff)
       
    def _box_line(self, text="", width=70):
        print("| " + text.ljust(width - 4) + " |")

    def print_invoice_box(self):
        WIDTH = 70

        print("+" + "-"*(WIDTH-2) + "+")
        self._box_line("HÓA ĐƠN BÁN HÀNG", WIDTH)
        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(self.store.name, WIDTH)
        self._box_line(f"Địa chỉ: {self.store.address}", WIDTH)
        self._box_line(f"ĐT: {self.store.phone}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(f"Tên khách hàng: {self.customer.name}", WIDTH)
        self._box_line(f"Địa chỉ: {self.customer.address}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        # Header bảng
        header = (
            f"{'STT':>3} | {'Tên hàng':<15} | {'SL':>6} | "
            f"{'Đơn giá':>12} | {'Thành tiền':>15}"
        )
        self._box_line(header, WIDTH)
        self._box_line("-"*66, WIDTH)

        # Dữ liệu bảng
        for idx, i in enumerate(self.item_list.items, start=1):
            row = (
                f"{idx:>3} | {i.name:<15} | {i.quantity:>6} | "
                f"{i.price:>12.2f} | {i.total:>15.2f}"
            )
            self._box_line(row, WIDTH)
        
        self._box_line("-"*66, WIDTH)

        t = self.item_list.total_row()
        total_row = (
            f"{'':>3} | {t['name']:<15} | {t['quantity']:>6} | "
            f"{t['price']:>12.2f} | {t['total']:>15.2f}"
        )
        self._box_line(total_row, WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")

        self._box_line(f"Tổng tiền: {self.item_list.sum_total():.2f}", WIDTH)
        self._box_line(f"{self.date} | {self.staff}", WIDTH)

        print("+" + "-"*(WIDTH-2) + "+")


if __name__ == "__main__":
    invoice = SalesInvoice()
    invoice.print_invoice_box()
```
# Quản lý phiếu nhập hàng
**Duck typing**
```python
from typing import Protocol

class Tax(Protocol):
    def tax(self):
        pass

class Item:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item
    
    @property
    def total_item(self):
        return self.price * self.quantity * self.t
    
    def tax(self):
        return 1.0

class Tivi(Item):
    def tax(self):
        return 0.5

class Fan(Item):
    def tax(self):
        return 0.6

class Mobi(Item):
    def tax(self):
        return 0.7
        
class Items:
    def __init__(self):
        self.items = [
            Tivi('TiVi', 30, 2),
            Fan("Quạt", 1.2, 3)
        ]
    
    def add_item(self, item: Item):
        self.items.append(item)
    
    def change(self, name = 'Quạt'):
        for item in self.items:
            if item.name == name:
                item.quantity = 5
    
    def remove(self, name='TiVi'):
        for i, item in enumerate(self.items):
            if item.name == name:
                self.items.pop(i)
                break

    def sum_total(self):    
        return sum(i.total for i in self.items)

class GoodsReceipt:
    def __init__(self, id_receipt, id_brand, address, date, name_brand):
        self.id_receipt = id_receipt
        self.id_brand = id_brand
        self.address = address
        self.date = date
        self.name_brand = name_brand
        self.table_items = Items()
    
    def print_receipt(self):
        print('\nPHIẾU NHẬP HÀNG')
        print("-" * 56)

        print(f"Mã phiếu: {self.id_receipt} {' '*20} Ngày lập: {self.date}")
        print(f"Mã NCC: {self.id_brand} {' '*20} Tên NCC: {self.name_brand}")
        print(f"Địa chỉ: {self.address}")
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'Đơn giá':>6} | {'Số lượng':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.table_items.items:
            print(f"{i.name:<15} | {i.price:>6} | {i.quantity:>12.2f} | {i.total:>15.2f}")

        print("-"*56)
        print("Tổng tiền:", self.table_items.sum_total())

def print_tax(t: Tax):
    print(t.tax())

if __name__ == "__main__": 
    receipt = GoodsReceipt(
        'PH001', 
        'NCC1', 
        "Khu công nghiệp Như Quỳnh A", 
        '1/1/2007', 
        'LG-Electronic'
    )
    
    print("Phiếu gốc")
    receipt.print_receipt()

    # thêm điện thoại vào phiếu
    mobi = Mobi("Mobi", 5, 10)
    receipt.table_items.add_item(mobi)
    print("Phiếu mới khi thêm")
    receipt.print_receipt()

    # Tìm đến Quạt và đổi số lượng thành 5 nếu có
    receipt.table_items.change()
    receipt.print_receipt()

    # xóa TiVi nếu có
    receipt.table_items.remove()
    receipt.print_receipt()
```
**Truyền thống**
```python
from abc import ABC, abstractmethod

class Item(ABC):
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
        self.t = self.tax()
        self.total = self.total_item

    @abstractmethod
    def tax(self):
        pass

    @property
    def total_item(self):
        return self.price * self.quantity * self.t
    
class Tivi(Item):
    def tax(self):
        return 0.5

class Fan(Item):
    def tax(self):
        return 0.6

class Mobi(Item):
    def tax(self):
        return 0.7

class Items:
    def __init__(self):
        self.items = []

    def add_item(self, item: Item):
        self.items.append(item)

    def sum_total(self):
        return sum(i.total for i in self.items)

class GoodsReceipt:
    def __init__(self, id_receipt, id_brand, address, date, name_brand):
        self.id_receipt = id_receipt
        self.id_brand = id_brand
        self.address = address
        self.date = date
        self.name_brand = name_brand
        self.items = Items()

    def print_receipt(self):
        print("\nPHIẾU NHẬP HÀNG")
        print("-" * 56)

        print(f"Mã phiếu: {self.id_receipt} {' '*20} Ngày lập: {self.date}")
        print(f"Mã NCC: {self.id_brand} {' '*20} Tên NCC: {self.name_brand}")
        print(f"Địa chỉ: {self.address}")
        print("-" * 56)

        print(f"{'Tên hàng':<15} | {'Đơn giá':>6} | {'Số lượng':>12} | {'Thành tiền':>15}")
        print("-" * 56)

        for i in self.items.items:
            print(f"{i.name:<15} | {i.price:>6} | {i.quantity:>12.2f} | {i.total:>15.2f}")

        print("-" * 56)
        print("Tổng tiền:", self.items.sum_total())

def print_tax(item: Item):
    print(item.tax())

if __name__ == "__main__":
    tivi = Tivi("TiVi", 30, 2)
    fan = Fan("Quạt", 1.2, 3)
    mobi = Mobi("Mobi", 5, 10)

    print_tax(tivi)
    print_tax(fan)
    print_tax(mobi)

    receipt = GoodsReceipt(
        "PH001",
        "NCC1",
        "Khu công nghiệp Như Quỳnh A",
        "1/1/2007",
        "LG-Electronic"
    )

    receipt.items.add_item(tivi)
    receipt.items.add_item(fan)
    receipt.items.add_item(mobi)

    receipt.print_receipt()
```
# Sơ đồ lớp (cầu thủ - người - câu lạc bộ)
```python
class Person:
    def __init__(self, name, age, country):
        self.name = name
        self.age = age
        self.country = country


class Player(Person):
    def __init__(self, player_id, name, age, country, position, jersey_number):
        super().__init__(name, age, country)
        self.player_id = player_id
        self.position = position
        self.jersey_number = jersey_number
        self.club = None          # Aggregation ◇

    def __str__(self):
        return (f"{self.player_id} | {self.name} | {self.age} | "
                f"{self.country} | {self.position} | {self.jersey_number}")

class Club:
    def __init__(self, club_id, name):
        self.club_id = club_id
        self.name = name
        self.players = []         # Aggregation ◇

    def add_player(self, player: Player):
        player.club = self
        self.players.append(player)

    def remove_player(self, player_id):
        self.players = [p for p in self.players if p.player_id != player_id]

    def show_players(self):
        for p in self.players:
            print(p)

if __name__ == "__main__":
    club = Club("C01", "Real Madrid")

    n = int(input("Number of players: "))
    for _ in range(n):
        p = Player(
            player_id=input("ID: "),
            name=input("Name: "),
            age=int(input("Age: ")),
            country=input("Country: "),
            position=input("Position: "),
            jersey_number=int(input("Jersey number: "))
        )
        club.add_player(p)

    print("\n--- Player List ---")
    club.show_players()
```
# Bài toán căn hộ OOP
```bash
1. Apartment (id_apartment, area, bedrooms, build_year, price, apartment_type)
```
```python
import math

class Apartment:
    def __init__(self, apartment_id, area, bedrooms, build_year, price, apartment_type):
        self.apartment_id = apartment_id
        self.area = area
        self.bedrooms = bedrooms
        self.build_year = build_year
        self.price = price
        self.apartment_type = apartment_type
    
    def __str__(self):
        return f"{self.apartment_id} {self.area} {self.bedrooms} {self.build_year} {self.price} {self.apartment_type}"
    
    def __eq__(self, other):
        return self.apartment_type == other.apartment_type and math.fabs(self.area - other.area) < 10
    
    def __add__(self, other):
        if self.apartment_type != other.apartment_type:
            raise ValueError("2 can ho khonh cung loai")
        
        return Apartment(
            'GOP_'+ self.apartment_id + other.apartment_id,
            self.area + other.area,
            self.bedrooms + other.bedrooms,
            max(self.build_year, other.build_year),
            self.price + other.price,           
            self.apartment_type
        )

def main():
    try:
        while True:
            n = int(input('n = '))

            if n > 3:
                break
        
        li = [Apartment(
            input('apartment_id: '),
            float(input('area: ')),
            int(input('bedrooms: ')),
            int(input('build_year: ')),
            float(input('price: ')),
            input('apartment_type: '),
        ) for _ in range(n)]

        with open('canho.txt', 'w') as f:
            for i in li:          
                print(i)
                f.write(f'{i}\n')
        
        apartment1 = Apartment('5', 12, 4, 2022, 12, '1pn')
        apartment2 = Apartment('5', 12, 4, 2022, 12, '1pn')
        print(apartment1 == apartment2)
        print(apartment1 + apartment2)
    except:
        print("Loi")

if __name__ == "__main__":
    main()
```
# phiếu đăng lý khóa học
```python
from abc import ABC, abstractmethod

class Course(ABC):
    def __init__(self, course_id, name, tuition, time):
        self.course_id = course_id
        self.name = name
        self.tuition = tuition
        self.time = time

    @abstractmethod
    def calc_total(self):
        pass

    def __str__(self):
        return f"{self.course_id:<15} | {self.name:<20} | {self.tuition:<5} | {self.time:<5} | {self.calc_total():<7}"

class NormalCourse(Course):
    def calc_total(self):
        return self.tuition * self.time

class DiscountCourse(Course):
    def calc_total(self):
        return self.tuition * self.time * 0.9

class Items:
    def __init__(self):
        self.li = [
            NormalCourse('KH001', 'Python cơ bản', 300, 6),
            NormalCourse('KH002', 'Lập trình web', 400, 5),
            NormalCourse('KH003', 'Khoa học dữ liệu', 500, 4)
        ]
    
    def find_time(self):
        return [row for row in self.li if row.time > 5]
    
    def sort_item(self):
        self.li.sort(key= lambda c : c.calc_total(), reverse=True)
    
    def build_receipt(self):
        lines = []
        lines.append(f"Mã phiếu: PH01{' '*20}Ngày đăng ký: 02/02/2026")
        lines.append(f"Mã học viên: HV01{' '*17}Tên học viên: Nguyễn Lan Anh")
        lines.append("Danh sách khóa học đăng ký")

        for c in self.li:
            lines.append(str(c))

        total = sum(c.calc_total() for c in self.li)
        lines.append(f"Tổng tiền: {total}".rjust(60))

        return "\n".join(lines)

    def display(self):
        print(self.build_receipt())
    
    def save_to_file(self, filename="phieu.txt"):
        with open(filename, "w", encoding="utf-8") as f:
            f.write(self.build_receipt())

def main():
    items = Items()

    print("Các khóa học có thời gian > 5:")
    for c in items.find_time():
        print(c)

    print("\nDanh sách sau khi sắp xếp:")
    items.sort_item()
    items.display()
    items.save_to_file()

if __name__ == "__main__":
    main()
```