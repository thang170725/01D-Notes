- [.init() (Khởi tạo tất cả module của pygame - window, keyboard, sound,...)](#init-khởi-tạo-tất-cả-module-của-pygame---window-keyboard-sound)
- [display](#display)
  - [set\_mode() (tạo cửa sổ game)](#set_mode-tạo-cửa-sổ-game)
    - [.fill() (Tô toàn bộ màn hình một màu)](#fill-tô-toàn-bộ-màn-hình-một-màu)
  - [.set\_caption() (Đặt tiêu đề cửa sổ)](#set_caption-đặt-tiêu-đề-cửa-sổ)
- [time](#time)
  - [Clock() (Đối tượng dùng để giới hạn FPS)](#clock-đối-tượng-dùng-để-giới-hạn-fps)
    - [.tick()](#tick)
- [event](#event)
  - [.get() (Lấy tất cả sự kiện vừa xảy ra)](#get-lấy-tất-cả-sự-kiện-vừa-xảy-ra)
  - [.type (Xem sự kiện thuộc loại gì)](#type-xem-sự-kiện-thuộc-loại-gì)
- [QUITE (Hằng số biểu diễn việc người dùng bấm nút X)](#quite-hằng-số-biểu-diễn-việc-người-dùng-bấm-nút-x)
- [.quit() (tắt pygame)](#quit-tắt-pygame)
- [raise SystemExit (Thoát chương trình)](#raise-systemexit-thoát-chương-trình)
---
# .init() (Khởi tạo tất cả module của pygame - window, keyboard, sound,...)
**Syn**
```bash
pygame.init()
```
**Ex**
```python
import pygame

pygame.init()

print("Done")
# Kết quả: Done 
# Lúc này pygame đã sẵn sàng sử dụng.
```
# display
## set_mode() (tạo cửa sổ game)
**Syn**
```bash
surface = pygame.display.set_mode((width, height))

- Output: Trả về một Surface (tấm vải để vẽ).
```
**Ex**
```python
screen = pygame.display.set_mode((500, 300))
# Kết quả
# +---------------------------+
# |                           |
# |      cửa sổ 500x300       |
# |                           |
# +---------------------------+
# Sau này mọi hình đều vẽ lên screen.
```
### .fill() (Tô toàn bộ màn hình một màu)
```bash
Nếu không gọi thì hình cũ sẽ còn nguyên.
```
**Syn**
```bash
screen.fill((R,G,B))
```
**Ex**
```python
screen.fill((255,0,0))
# Kết quả
# ██████████████
# Màn hình đỏ.
# ██████████████
```
## .set_caption() (Đặt tiêu đề cửa sổ)
**Syn**
```bash
pygame.display.set_caption("Tên cửa sổ")
```
**Ex**
```python
pygame.display.set_caption("My Game")
# Kết quả: Thanh tiêu đề sẽ hiện My Game
```
# time
## Clock() (Đối tượng dùng để giới hạn FPS)
```bash
clock = pygame.time.Clock()
```
### .tick()
**Ex**
```python
clock = pygame.time.Clock()

clock.tick(60)
# Nghĩa là Không cho game chạy quá 60 FPS.
```
# event
## .get() (Lấy tất cả sự kiện vừa xảy ra)
```bash
Ví dụ
    - nhấn phím
    - rê chuột
    - đóng cửa sổ
```
**Syn**
```bash
events = pygame.event.get()

- Output: Trả về list.
```
**Ex**
```python
for event in pygame.event.get():
    print(event)

# Nếu bấm chuột
# MouseButtonDown
# Nếu nhấn A
# KeyDown
```
## .type (Xem sự kiện thuộc loại gì)
```python
for event in pygame.event.get():
    print(event.type)
# QUIT
# KEYDOWN
# MOUSEBUTTONDOWN
```
# QUITE (Hằng số biểu diễn việc người dùng bấm nút X)
# .quit() (tắt pygame)
```python
if event.type == pygame.QUIT:
    pygame.quit()
# Nếu bấm X Game sẽ đóng.
```
# raise SystemExit (Thoát chương trình)
**Ex**
```python
raise SystemExit
#  Kết quả Python kết thúc luôn.
```
11. pygame.draw.circle()
Chức năng

Vẽ hình tròn.

Đây là hàm quan trọng nhất trong project của bạn.

Cú pháp
pygame.draw.circle(
    surface,
    color,
    center,
    radius
)
Ví dụ
pygame.draw.circle(
    screen,
    (255,0,0),
    (100,100),
    30
)

Ý nghĩa

surface = screen

màu = đỏ

tọa độ = (100,100)

bán kính = 30

Kết quả

      ●

Một hình tròn đỏ.

12. pygame.display.flip()
Chức năng

Cập nhật màn hình.

Nếu không gọi thì bạn đã vẽ nhưng cửa sổ không đổi.

Cú pháp
pygame.display.flip()
Ví dụ
screen.fill((255,0,0))

pygame.display.flip()

Kết quả

Màn hình chuyển sang màu đỏ.

13. clock.tick()
Chức năng

Giới hạn FPS.

Cú pháp
clock.tick(60)
Ví dụ
while True:

    ...

    clock.tick(30)

Game chạy

30 FPS

Nếu

clock.tick(120)

Game chạy tối đa

120 FPS