- [sync\_api](#sync_api)
  - [sync\_playwright](#sync_playwright)
    - [chromium](#chromium)
    - [firefox](#firefox)
      - [.launch()](#launch)
- [page.goto() (Điều hướng trình duyệt đến một trang web cụ thể)](#pagegoto-điều-hướng-trình-duyệt-đến-một-trang-web-cụ-thể)
- [Cách vượt cloudfare](#cách-vượt-cloudfare)
- [mở các tab mới](#mở-các-tab-mới)
- [page.wait\_for\_selector()](#pagewait_for_selector)
  - [Demo ví dụ về wait\_for\_select](#demo-ví-dụ-về-wait_for_select)
- [page.wait\_for\_timeout() \& page.wait\_for\_load\_state()](#pagewait_for_timeout--pagewait_for_load_state)
- [.launch\_persistent\_context()](#launch_persistent_context)
- [.new\_page() (dùng để mở một tab mới trong cùng một browser context)](#new_page-dùng-để-mở-một-tab-mới-trong-cùng-một-browser-context)
- [page.locator()](#pagelocator)
  - [.nth()](#nth)
  - [.inner\_text()](#inner_text)
  - [.get\_attribute()](#get_attribute)
  - [.count()](#count)
---
# sync_api
## sync_playwright
### chromium
### firefox 
#### .launch()
**Syn**
```bash
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
```
**Ex: Mở firefox và vào Google**
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.firefox.launch(
        headless=False 
    )

    context = browser.new_context()

    page = context.new_page()
    page.goto("https://www.google.com")
    page.wait_for_timeout(5000)

    browser.close()
```
# page.goto() (Điều hướng trình duyệt đến một trang web cụ thể)
**Syn**
```bash
await page.goto("đường_dẫn_url")

- url (Bắt buộc)    : Địa chỉ trang web bạn muốn truy cập. Lưu ý: Phải có đầy đủ giao thức http:// hoặc https://
- wait_until (Quan trọng nhất): Đây là tham số quyết định Playwright sẽ đợi đến thời điểm nào thì mới chạy câu lệnh tiếp theo. 
    + 'domcontentloaded': Đợi cho đến khi cấu trúc HTML được tải xong.Khi bạn chỉ cần lấy chữ, không quan tâm đến ảnh hay CSS. Rất nhanh.
    + 'load' (Mặc định): Đợi cho đến khi toàn bộ trang web, ảnh, và các file CSS tải xong. Khi trang web đơn giản, không có nhiều hiệu ứng phức tạp.
    + 'networkidle' : Đợi cho đến khi không còn yêu cầu mạng nào trong ít nhất 500ms. Nên dùng: Khi trang web dùng Javascript để tải dữ liệu (như Facebook, Shopee, Batdongsan).
- timeout: Thời gian tối đa (tính bằng mili giây) mà Playwright sẽ đợi trang web tải. Nếu quá thời gian này trang chưa xong, nó sẽ báo lỗi (Crash). Mặc định: 30,000 ms (30 giây).
- referer: Giả lập rằng bạn đến từ một trang web khác (ví dụ: giả vờ như bạn bấm vào link này từ Google).Ứng dụng: Vượt qua một số hệ thống chống cào dữ liệu (Anti-crawl).
```
**Ex**
```python
import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False)
        page = await browser.new_page()

        # SỬ DỤNG GOTO VỚI CÁC THAM SỐ
        await page.goto(
            "https://batdongsan.com.vn", 
            wait_until="networkidle", # Đợi cho đến khi mạng "rảnh", dữ liệu tải hết
            timeout=10000,            # Chỉ đợi tối đa 10 giây, quá 10s là bỏ qua
            referer="https://www.google.com" # Giả vờ đến từ Google
        )

        print("Trang web đã tải xong hoàn toàn!")
        await browser.close()

asyncio.run(main())
```
```bash
- Các hành vi né bot
    + persistent profile
    + stealth
    + hành vi người thật
```
# Cách vượt cloudfare
```text
luôn luôn truy cập vào trang web 1 lần trước để giải hết capcha.
```
**Step 1**
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=False,
        args=[
            "--disable-blink-features=AutomationControlled",
            "--start-maximized"
        ]
    )

    page = browser.new_page()
    page.goto("https://batdongsan.com.vn")

    input("👉 Giữ browser mở. Khi bạn xác minh xong Cloudflare thì nhấn Enter...")
    browser.close()
```
**Step 2**
```text
gen code hoặc tự việt code.
```

# mở các tab mới
```python
from playwright.async_api import async_playwright

async def demo():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False)
        context = await browser.new_context()

        page1 = await context.new_page()
        await page1.goto("https://example.com")

        # mở tab mới
        page2 = await context.new_page()
        await page2.goto("https://playwright.dev")
        await browser.close()

# 2 tab mở song song
# Dùng chung cookie / login
```
# page.wait_for_selector()
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")

    # Chờ element xuất hiện trên DOM
    page.wait_for_selector("textarea[name='q']")

    print("Ô tìm kiếm đã sẵn sàng")

    page.wait_for_timeout(3000)
    browser.close()
```
## Demo ví dụ về wait_for_select
```bash
Dưới đây là ví dụ kết hợp các hàm cơ bản nhất với wait_for_selector. Ví dụ này sẽ truy cập vào trang Wikipedia, đợi ô tìm kiếm xuất hiện và lấy nội dung tiêu đề trang.
```
```python
from playwright.async_api import async_playwright

async def run():
    async with async_playwright() as p:
        # 1. Mở trình duyệt
        browser = await p.chromium.launch(headless=False)
        page = await browser.new_page()

        # 2. Đi tới trang web
        await page.goto("https://vi.wikipedia.org/")

        # 3. Đợi cho đến khi phần tử "Tiêu đề chào mừng" xuất hiện trên màn hình
        # Class CSS của tiêu đề Wikipedia là '#mp-welcome'
        await page.wait_for_selector("#mp-welcome")

        # 4. Tìm phần tử đó bằng locator
        welcome_msg = page.locator("#mp-welcome")

        # 5. Lấy nội dung chữ và in ra
        text = await welcome_msg.inner_text()
        print(f"Nội dung tìm được: {text}")

        # Đóng trình duyệt
        await browser.close()

asyncio.run(run())
```
# page.wait_for_timeout() & page.wait_for_load_state()
- [sync\_api](#sync_api)
  - [sync\_playwright](#sync_playwright)
    - [chromium](#chromium)
    - [firefox](#firefox)
      - [.launch()](#launch)
- [page.goto() (Điều hướng trình duyệt đến một trang web cụ thể)](#pagegoto-điều-hướng-trình-duyệt-đến-một-trang-web-cụ-thể)
- [Cách vượt cloudfare](#cách-vượt-cloudfare)
- [mở các tab mới](#mở-các-tab-mới)
- [page.wait\_for\_selector()](#pagewait_for_selector)
  - [Demo ví dụ về wait\_for\_select](#demo-ví-dụ-về-wait_for_select)
- [page.wait\_for\_timeout() \& page.wait\_for\_load\_state()](#pagewait_for_timeout--pagewait_for_load_state)
- [.launch\_persistent\_context()](#launch_persistent_context)
- [.new\_page() (dùng để mở một tab mới trong cùng một browser context)](#new_page-dùng-để-mở-một-tab-mới-trong-cùng-một-browser-context)
- [page.locator()](#pagelocator)
  - [.nth()](#nth)
  - [.inner\_text()](#inner_text)
  - [.get\_attribute()](#get_attribute)
  - [.count()](#count)
---

# .launch_persistent_context()
```bash
- Đây là cách sử dụng profile thật để chống bot.
- Các website hiện đại đều có cơ chế chống bot vô cùng mạnh nên cần một số kỹ thuật mới có thể crawl dữ liệu thành công.
```
**Syn**
```bash
browser = p.chromium.launch_persistent_context(
    user_data_dir="/home/thang/pw-chrome-profile",
    headless=False,
    args=[
            "--disable-blink-features=AutomationControlled",
            "--start-maximized",
            "--disable-css"
    ]
)

- args: 
    + --disable-blink-features=AutomationControlled : để che navigator.webdriver
    + --start-maximized                             : để mở cửa sổ to
    + --disable-css                                 : không load css
    + --disable-images                              : không load ảnh
```
**Ex**
```python
from playwright.async_api import Playwright, BrowserContext

async def create_browser_context(
    p: Playwright,
    profile_dir: str = '/home/thang/pw-chrome-profile',
    headless: bool = False
 ) -> BrowserContext:
    return await p.chromium.launch_persistent_context(
        user_data_dir=profile_dir,
        headless=False,
        args=[
            "--disable-blink-features=AutomationControlled",
            "--disable-images",
            "--disable-css",
            "--start-maximized"
        ]
    )
```
# .new_page() (dùng để mở một tab mới trong cùng một browser context)
**Khi nào thì dùng new_page?**
```bash
- Website mở link sang tab mới
- Test nhiều user / nhiều màn hình trong cùng session
- So sánh dữ liệu giữa 2 trang
- Popup / OAuth / Payment / External link
```
- [page.locator()](#pagelocator)
  - [.nth()](#nth)
  - [.inner\_text()](#inner_text)
  - [.get\_attribute()](#get_attribute)
  - [.count()](#count)
---
# page.locator()
```bash
Tác dụng: Tạo ra một "vật trỏ" để tìm kiếm các phần tử trên trang (như nút bấm, ô nhập liệu, thẻ văn bản). Nó chưa lấy dữ liệu ngay mà chỉ xác định vị trí.
```
**Syn**
```bash
element = page.locator("tên_thẻ_hoặc_class_css")
```
**Ex**
```python
tieu_de = page.locator("h1") # Tìm tất cả các thẻ h1 trên trang
```
## .nth()
```bash
- Tác dụng: Chọn phần tử thứ n trong danh sách các phần tử tìm được (bắt đầu từ số 0).
```
**Syn** 
```bash
item = element.nth(0) (lấy phần tử đầu tiên).
```
**Ex**
```python
danh_sach = page.locator("li")
thu_nhat = danh_sach.nth(0) # Lấy dòng đầu tiên trong danh sách
```
## .inner_text()
```bash
Lấy nội dung chữ bên trong một phần tử.
```
**Syn**
```bash
chu = await element.inner_text()
```
**Ex**
```python
doan_van = page.locator("p") # Giả sử có thẻ <p>Chào bạn</p>
noidung = await doan_van.inner_text()
print(noidung) # Kết quả: Chào bạn
```
## .get_attribute()
```bash
- Lấy giá trị của một thuộc tính trong thẻ (thường dùng nhất là lấy link href hoặc link ảnh src).
```
**Syn** 
```bash
gia_tri = await element.get_attribute("tên_thuộc_tính")
```
**Ex**
```python
the_link = page.locator("a") # Lấy đường link của một thẻ <a>
url = await the_link.get_attribute("href")

print(url)
```
## .count()
```bash
- Đếm xem có bao nhiêu phần tử khớp với locator đã tìm.
```
**Syn** 
```bash
so_luong = await element.count()
```
**Ex**
```python
cac_nut = page.locator("button")
print(await cac_nut.count()) # In ra số lượng nút bấm có trên trang
```