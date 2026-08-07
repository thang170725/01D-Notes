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
Câu trả lời ngắn là:

Có, Pygame cần cài thêm.
Có thể làm game thương mại, nhưng không phải là lựa chọn phổ biến cho game thương mại hiện nay.
1. Có cần cài không?

Có.

Pygame không nằm trong thư viện chuẩn của Python.

Cài bằng:

pip install pygame

Kiểm tra:

import pygame

print(pygame.version.ver)
2. Pygame là gì?

Pygame là một thư viện giúp Python có thể:

tạo cửa sổ game
vẽ hình
hiển thị sprite
phát nhạc
phát hiệu ứng âm thanh
xử lý bàn phím
xử lý chuột
kiểm tra va chạm
quản lý FPS

Ví dụ

pygame.init()

screen = pygame.display.set_mode((800,600))

while True:
    ...

Nó cung cấp gần như những thứ cơ bản nhất để viết game.

3. Có làm được game thương mại không?

Có.

Pygame không hề giới hạn bạn.

Bạn có thể làm

game bán trên Steam
game bán trên itch.io
game phát hành miễn phí

đều được.

Ví dụ có khá nhiều game indie được viết bằng Pygame.

4. Nhưng tại sao ít công ty dùng?

Vì Pygame khá "thấp".

Nó chỉ giúp bạn

Tạo cửa sổ

↓

Đọc bàn phím

↓

Vẽ hình

Còn tất cả những thứ khác bạn phải tự làm.

Ví dụ

Muốn có animation

↓

tự code.

Muốn particle

↓

tự code.

Muốn lighting

↓

tự code.

Muốn camera

↓

tự code.

Muốn UI

↓

tự code.

5. Unity thì khác

Ví dụ Unity

Animation

Physics

Particle

Lighting

Tilemap

UI

Audio

Navigation

AI

Profiler

Build Android

Build IOS

đều có sẵn.

6. Pygame phù hợp game nào?

Rất mạnh với

Game 2D

Ví dụ

Mario
Flappy Bird
Snake
Tetris
Breakout
Tower Defense
RPG 2D
Pokemon clone

Ví dụ

□□□□□□□□□□

😀

👾

💰

Pygame làm rất tốt.

7. Còn game 3D?

Pygame gần như không dành cho 3D.

Muốn 3D

thường phải kết hợp

OpenGL
ModernGL
Panda3D
Ursina

hoặc dùng Unity / Unreal.

8. Hiệu năng

Rất nhiều người nghĩ

Python chậm → game sẽ chậm.

Không hẳn.

Ví dụ game

Snake

Flappy Bird

Pacman

2048

Sudoku

Chess

chạy cực kỳ mượt.

Nhưng game kiểu

GTA

PUBG

Valorant

Black Myth Wukong

thì không.

9. Có game nổi tiếng dùng Pygame không?

Có khá nhiều game indie.

Ngoài ra Pygame được dùng rất nhiều trong

giáo dục
trường đại học
dạy AI Game
Game Jam
prototype

Vì code rất nhanh.

10. Nếu muốn làm game bán được?

Hoàn toàn được.

Ví dụ game

Roguelike

Visual Novel

Puzzle

Platform

RPG 2D

Turn-based

Card Game

Pygame đều làm được.

Nếu gameplay hay thì vẫn bán tốt.

11. Khi nào nên học Pygame?

Theo mình, nếu mục tiêu của bạn là:

học lập trình game,
hiểu game loop,
hiểu xử lý sự kiện,
quản lý sprite, va chạm, animation,
hoặc làm các game 2D đơn giản đến trung bình,

thì Pygame là lựa chọn rất tốt vì bạn sẽ hiểu cách game hoạt động "từ bên trong".

Nếu mục tiêu là:

làm game 3D,
game mobile quy mô lớn,
game có đồ họa hiện đại,
hoặc muốn xin việc vào các studio game,

thì nên học các game engine như Unity (C#) hoặc Unreal Engine (C++/Blueprint), vì đó là những công cụ được ngành công nghiệp sử dụng rộng rãi.

Tóm lại, Pygame không chỉ là "đồ chơi". Nó đủ mạnh để tạo ra các game 2D hoàn chỉnh và thậm chí có thể thương mại hóa. Tuy nhiên, với các dự án lớn, engine chuyên dụng sẽ giúp bạn phát triển nhanh hơn vì đã tích hợp sẵn rất nhiều tính năng mà Pygame yêu cầu bạn tự xây dựng.
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