# page.goto()
```bash
- Tác dụng: Điều hướng trình duyệt đến một trang web cụ thể.
- Nó có các tham số (parameters) rất quan trọng để giúp bạn kiểm soát việc "Khi nào thì coi như trang web đã tải xong?".
```
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