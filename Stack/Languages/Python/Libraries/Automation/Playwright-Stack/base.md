- [Directory structure](#directory-structure)
- [Set up](#set-up)
- [gencode](#gencode)
- [khi nào thì dùng playwright.async\_api, sync\_api](#khi-nào-thì-dùng-playwrightasync_api-sync_api)
- [Sơ đồ một browser automation](#sơ-đồ-một-browser-automation)
- [mở web bằng profile thật](#mở-web-bằng-profile-thật)
- [page.is\_visible() \& page.is\_enabled() \& locator.is\_visible()](#pageis_visible--pageis_enabled--locatoris_visible)
- [page.text\_content() \& page.inner\_text()](#pagetext_content--pageinner_text)
- [page.pause() # slow\_mo # print()](#pagepause--slow_mo--print)
  - [pause để xem từng bước](#pause-để-xem-từng-bước)
- [page.mouse.move() \& page.mouse.click() \& page.keyboard.press()](#pagemousemove--pagemouseclick--pagekeyboardpress)
  - [di chuyển chuột](#di-chuyển-chuột)
- [page.locator() \& locator.click() \& locator.fill()](#pagelocator--locatorclick--locatorfill)
  - [search google](#search-google)
  - [Mở youtube -\> search -\> click -\> skip ads](#mở-youtube---search---click---skip-ads)
- [page.mouse.wheel()](#pagemousewheel)

---
# Directory structure
```bash
Browser-Automation/
├── 01_Browser_Context.md     # Quản lý, Khởi tạo Browser, Context, New Page, Async API
├── 02_Navigation_Waiting.md  # Điều hướng, đợi trang
├── 03_Locators_Actions.md    # Liên quan đến locator
├── 04_AntiBot_Stealth.md     # Playwright-stealth, bypass cloudflare, antibot
├── 05_Scraping_Crawling.md   # Logic cào dữ liệu, xử lý bảng, scroll trang
└── 06_Debug_Tooling.md       # Debug mode, Playwright Inspector, Trace Viewer
```
```bash
Để hiểu cách hoạt động của Playwright một cách đơn giản nhất, bạn có thể tưởng tượng nó như một người dùng thật: Mở trình duyệt -> Đợi trang hiện ra -> Tìm thứ mình cần -> Lấy thông tin.
```
# Set up
```bash
pip install playwright
playwright install
```

# gencode
```bash
- playwright codegen https://example.com
- playwright codegen --target python https://youtube.com
```

# khi nào thì dùng playwright.async_api, sync_api
```bash
Playwright Python có 2 cách dùng:
API	        Cách chạy	                Đặc điểm
async_api	Bất đồng bộ (async/await)	Mạnh, nhanh, chuyên nghiệp
sync_api	Đồng bộ (chạy từng bước)	Dễ học, dễ đọc
```
**Ex**
```bash
- Sync (đồng bộ): Làm xong việc A → mới làm B
    1. Đi mua cà phê
    2. Uống xong
    3. Rồi mới đi làm
- Async (bất đồng bộ). Trong lúc chờ A → có thể làm B
    1. Order cà phê
    2. Trong lúc chờ → check mail
    3. Cà phê xong → uống
```
**Khi nào dùng sync_api?**
```bash
- Mới học Playwright
- Viết script đơn giản
- Debug test
- Test nhỏ, chạy local
- Không cần chạy song song
- Ưu điểm:
    + Code dễ đọc
    + Ít lỗi logic
    + Không cần async / await
```
**Khi nào dùng async_api?**
```bash
- Project lớn
- Chạy nhiều test
- Cần chạy song song
- Tích hợp CI/CD
- Kết hợp với framework async (FastAPI, asyncio)
- Ưu điểm:
    + Nhanh hơn
    + Scale tốt
    + Chuẩn production
```
# Sơ đồ một browser automation
```bash
browser
 └── context (cookie, session riêng)
      ├── page 1
      ├── page 2  ← new_page
      └── page 3
```


# mở web bằng profile thật
Cách setup profile thật [link](../base.md)
```python
from playwright.sync_api import sync_playwright

USER_DATA_DIR = "/home/thang/pw-firefox-profile"

with sync_playwright() as p:
    context = p.firefox.launch_persistent_context(
        user_data_dir=USER_DATA_DIR,
        headless=False
    )

    page = context.pages[0]
    page.goto("https://batdongsan.com.vn/nha-dat-ban-ha-noi")

    print("👉 Login xong rồi quay lại terminal nhấn Enter") # sau khi login xong, Enter mới đóng
    input()
```
# page.is_visible() & page.is_enabled() & locator.is_visible()
# page.text_content() & page.inner_text() 
 NHÓM DEBUG – HỌC NHANH X10. Khi mới học → luôn bật.

# page.pause() # slow_mo # print()
## pause để xem từng bước
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=False,
        slow_mo=500  # chậm từng hành động
    )

    page = browser.new_page()
    page.goto("https://google.com")

    # Dừng lại để inspect
    page.pause()

    browser.close()
```
- NHÓM CHUỘT & BÀN PHÍM – GIỐNG NGƯỜI THẬT. Dùng để vượt web khó

# page.mouse.move() & page.mouse.click() & page.keyboard.press()
## di chuyển chuột
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://example.com")

    # Di chuyển chuột tới tọa độ
    page.mouse.move(400, 300)

    # Click chuột trái
    page.mouse.click(400, 300)

    page.wait_for_timeout(3000)
    browser.close()
```
- [page.locator() \& locator.click() \& locator.fill() \& locator.count()](#pagelocator--locatorclick--locatorfill--locatorcount)
  - [search google](#search-google)

---

```text
- NHÓM LOCATOR – CHUẨN PLAYWRIGHT MỚI. RẤT QUAN TRỌNG – nên dùng thay selector cũ.
- Vì sao locator tốt hơn?
  + Tự wait
  + Ít lỗi
  + Code rõ ràng
```

# page.locator() & locator.click() & locator.fill()
## search google
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")

    # Tạo locator
    search_box = page.locator("textarea[name='q']")

    # Chờ locator sẵn sàng
    search_box.wait_for()

    # Gõ chữ
    search_box.fill("locator playwright python")

    # Enter
    search_box.press("Enter")

    page.wait_for_timeout(5000)
    browser.close()
```
**Ex2**
```python
from playwright.sync_api import sync_playwright
import random
import time

with sync_playwright() as p:
    browser = p.chromium.launch(
        headless=False,
        slow_mo=50  # làm chậm hành động
    )

    context = browser.new_context(
        user_agent=(
            "Mozilla/5.0 (X11; Linux x86_64) "
            "AppleWebKit/537.36 (KHTML, like Gecko) "
            "Chrome/120.0.0.0 Safari/537.36"
        ),
        viewport={"width": 1366, "height": 768},
        locale="vi-VN"
    )

    page = context.new_page()

    # 🔥 Xóa dấu hiệu webdriver
    page.add_init_script("""
        Object.defineProperty(navigator, 'webdriver', {
            get: () => undefined
        });
    """)

    # Vào Google
    page.goto("https://www.google.com", wait_until="domcontentloaded")

    # Nghỉ như người suy nghĩ
    time.sleep(random.uniform(2, 4))

    search_box = page.locator("textarea[name='q']")
    search_box.wait_for()

    # Gõ từng chữ (giống người)
    search_box.click()
    for char in "playwright python tutorial":
        search_box.type(char)
        time.sleep(random.uniform(0.05, 0.2))

    search_box.press("Enter")

    page.wait_for_timeout(5000)
    browser.close()
```

from playwright.sync_api import sync_playwright

USER_DATA_DIR = "/home/thang/pw-firefox-profile"

with sync_playwright() as p:
    context = p.firefox.launch_persistent_context(
        user_data_dir=USER_DATA_DIR,
        headless=False,
        viewport={"width": 1280, "height": 800}
    )

    page = context.pages[0] if context.pages else context.new_page()
    page.goto("https://www.youtube.com", wait_until="domcontentloaded")

    search_box = page.locator("input[name='search_query']:not([hidden])")
    search_box.wait_for(state="visible", timeout=30000)

    search_box.fill("locator playwright python")
    search_box.press("Enter")

    page.wait_for_timeout(5000)

    print("👉 Login xong rồi quay lại terminal nhấn Enter")
    input()

    context.close()

from playwright.sync_api import sync_playwright
import time
import random


def human_type(page, locator, text):
    locator.click()
    time.sleep(0.5)
    for ch in text:
        page.keyboard.type(ch)
        time.sleep(random.uniform(0.12, 0.22))


def human_scroll(page):
    page.mouse.wheel(0, random.randint(700, 1000))
    time.sleep(random.uniform(1.0, 1.6))


def skip_ads_if_any(page):
    try:
        skip_btn = page.locator(
            "button.ytp-ad-skip-button, button:has-text('Skip')"
        )
        skip_btn.wait_for(timeout=15000)
        skip_btn.click()
        print("⏭ Đã skip quảng cáo")
    except:
        print("ℹ️ Không có quảng cáo")


with sync_playwright() as p:
    context = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=False
    )

    page = context.pages[0]

    # 1️⃣ Mở YouTube
    page.goto("https://www.youtube.com", wait_until="domcontentloaded")
    page.wait_for_load_state("networkidle")
    print("🌐 Đã mở YouTube")

    # 2️⃣ Search
    search_box = page.locator('input[name="search_query"]')
    print("⏳ Đợi search box...")
    search_box.wait_for(state="visible", timeout=60000)

    human_type(page, search_box, "list edm hot doyin")
    print("🔎 Đã gõ xong")
    search_box.press("Enter")

    # 3️⃣ Đợi trang kết quả
    page.wait_for_load_state("networkidle")
    time.sleep(2)

    # 4️⃣ Scroll cho đến khi có đủ 10 video THẬT
    videos = page.locator("ytd-video-renderer")
    round_scroll = 0

    while videos.count() < 10:
        human_scroll(page)
        round_scroll += 1
        print(f"🔄 Scroll {round_scroll}, video hiện có: {videos.count()}")

        if round_scroll > 12:
            raise Exception("❌ Không tìm đủ 10 video")

    print("✅ Đã đủ video")

    # 5️⃣ CLICK VIDEO THỨ 10 (CLICK LINK THẬT)
    video_10 = videos.nth(9)
    video_link = video_10.locator("a#thumbnail")

    video_link.scroll_into_view_if_needed()
    time.sleep(1)

    video_link.click()
    print("▶️ Đã click video thứ 10")

    # 6️⃣ ĐỢI VÀO TRANG /watch
    page.wait_for_url("**/watch**", timeout=30000)
    print("🎬 Đã vào trang xem video")

    # 7️⃣ ĐỢI VIDEO ELEMENT THẬT
    video_tag = page.locator("video.html5-main-video")
    video_tag.wait_for(state="visible", timeout=30000)
    print("🎵 Video đang phát")

    time.sleep(3)

    # 8️⃣ Skip quảng cáo nếu có
    skip_ads_if_any(page)

    input("⏸ Đang phát nhạc, nhấn Enter để thoát")
    context.close()
```text
- get_by_role là cách chọn (locator) “xịn” nhất của Playwright, dựa trên ARIA accessibility role thay vì CSS/XPath. Nó ổn định – ít vỡ – giống cách người dùng thật tương tác.
- get_by_role dùng để tìm element theo vai trò (role) giao diện, ví dụ: button, textbox, ...
- Nó không phụ thuộc class/id → web đổi CSS vẫn chạy.
- Vấn đề: Dev đổi class → chết, XPath -> Dài, khó đọc
-> get_by_role: Chuẩn web, ổn định. Playwright khuyên dùng số 1
```
**Syn**
```bash
page.get_by_role(role, **options)
- role
    + button    : nút
    + textbox	: input text
    + link	    : thẻ a
    + heading   : h1–h6
    + checkbox	: checkbox
    + radio	    : radio
    + combobox	: select
    + menuitem	: item menu
    + dialog	: modal
```

## Mở youtube -> search -> click -> skip ads
```python
from playwright.sync_api import sync_playwright
import re

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.youtube.com/")

    search = page.get_by_role("combobox", name="Search")
    search.fill("list edm hot tiktok")
    search.press("Enter")

    # đợi list video load
    page.wait_for_selector("ytd-video-renderer")

    first_video = page.locator("ytd-video-renderer").first
    first_video.scroll_into_view_if_needed()
    first_video.click()

    # đợi video player
    page.wait_for_selector("video")

    try:
        skip = page.get_by_role(
            "button",
            name=re.compile("Skip|Bỏ qua", re.I)
        )
        skip.wait_for(timeout=35000)
        skip.click()
    except:
        print("Không có quảng cáo hoặc không skip được")


    page.keyboard.press("Enter")

    input("👉 Nhấn Enter để đóng browser...")
    browser.close()
```
# page.mouse.wheel()
```bash
- page.mouse.wheel(dx, dy) dùng để giả lập thao tác lăn chuột (scroll) trên trang web.
- Thường dùng khi:
    + Trang không scroll được bằng page.evaluate
    + Test lazy loading, infinite scroll
    + Giả lập hành vi người dùng thật
```
**Syn**
```bash
await page.mouse.wheel(deltaX, deltaY)

- deltaX	: Scroll ngang (trái/phải)
- deltaY	: Scroll dọc (lên/xuống)
- Giá trị dương = scroll xuống / sang phải
- Giá trị âm = scroll lên / sang trái
```
3️⃣ Demo cơ bản – scroll xuống trang
import { chromium } from '@playwright/test';

const browser = await chromium.launch();
const page = await browser.newPage();

await page.goto('https://example.com');

// Scroll xuống 500px
await page.mouse.wheel(0, 500);

await browser.close();

4️⃣ Scroll nhiều lần (mô phỏng người dùng)
for (let i = 0; i < 5; i++) {
  await page.mouse.wheel(0, 300);
  await page.waitForTimeout(500); // đợi load nội dung
}


➡️ Rất hay dùng cho infinite scroll

5️⃣ Scroll lên
await page.mouse.wheel(0, -400);

6️⃣ Scroll ngang (carousel, bảng rộng)
await page.mouse.wheel(300, 0);

7️⃣ Scroll tại vị trí cụ thể (quan trọng ⚠️)

mouse.wheel scroll tại vị trí con trỏ chuột, vì vậy nên move chuột trước

// Di chuyển chuột vào giữa màn hình
await page.mouse.move(500, 400);

// Scroll
await page.mouse.wheel(0, 600);

8️⃣ Demo scroll đến khi load xong (infinite scroll)
let previousHeight = 0;

while (true) {
  const currentHeight = await page.evaluate(() => document.body.scrollHeight);
  if (currentHeight === previousHeight) break;

  previousHeight = currentHeight;
  await page.mouse.wheel(0, 1000);
  await page.waitForTimeout(1000);
}

9️⃣ So sánh với cách scroll khác
Cách	Khi nào dùng
page.mouse.wheel	Mô phỏng người dùng thật
page.evaluate(() => window.scrollTo())	Scroll nhanh, đơn giản
locator.scrollIntoViewIfNeeded()	Scroll tới element cụ thể

Ví dụ scroll tới element (khuyên dùng nếu có selector):

await page.locator('#footer').scrollIntoViewIfNeeded();

10️⃣ Lỗi thường gặp ❌
❌ Scroll nhưng trang không di chuyển

➡️ Do chuột chưa nằm trong vùng scroll

✅ Fix:

await page.mouse.move(100, 100);
await page.mouse.wheel(0, 500);


Nếu bạn đang:

Test React / Vue infinite scroll

Scroll trong modal / div có overflow

Dùng Playwright Test (test() syntax)

👉 gửi mình case cụ thể, mình viết demo đúng chuẩn cho bạn nhé 🚀

import asyncio
from playwright.async_api import async_playwright

async def main():
    async with async_playwright() as p:
        context = await p.chromium.launch_persistent_context(
            user_data_dir="/home/thang/pw-chrome-profile",
            headless=False,
            args=[
                "--disable-blink-features=AutomationControlled",

                # 🔥 Màn desktop 1360x768 ở PHÍA TRÊN
                "--window-size=1360,768",
                # "--window-position=0,-768"
            ],
            viewport=None
        )

        page = await context.new_page()
        await page.goto("https://www.youtube.com/", timeout=60000)

        # Chuột giữa màn desktop
        await page.mouse.move(680, 384)

        # Scroll chậm, thấy rõ
        for _ in range(25):
            await page.mouse.wheel(0, 80)
            await page.wait_for_timeout(200)

        await page.wait_for_timeout(5000)
        await context.close()

asyncio.run(main())
