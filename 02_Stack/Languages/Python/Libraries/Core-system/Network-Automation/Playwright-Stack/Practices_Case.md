```text
- Các kỹ thuật crawl dữ liệu
    + listing vs detail
    + crawl theo label
    + field missing → None    
    + pipeline
```

# crawl bằng sync
## demo craw dữ liệu trên trang bất động sản
```python
from playwright.sync_api import sync_playwright

BASE_URL = "https://batdongsan.com.vn"
URL = "https://batdongsan.com.vn/ban-nha-dat-ba-dinh/gia-tren-60-ty"

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

    page.goto(URL, wait_until="domcontentloaded")
    page.wait_for_selector("a.js__product-link-for-product-id")

    cards = page.locator("a.js__product-link-for-product-id")
    count = min(cards.count(), 3)

    for i in range(count):
        card = cards.nth(i)

        link = card.get_attribute("href")
        title = card.locator("span.pr-title").inner_text()

        price = card.locator("span.re__card-config-price").inner_text()
        area = card.locator("span.re__card-config-area").inner_text()

        print("==========")
        print("Title:", title.strip())
        print("Price:", price)
        print("Area:", area)
        print("Link:", BASE_URL + link)

    browser.close()
```

## demo crawl detail trên trang bất động sản
from playwright.sync_api import sync_playwright

URL = "https://batdongsan.com.vn/ban-nha-mat-pho-duong-nguyen-khac-hieu-phuong-truc-bach/ban-toa-ba-dinh-222m2-10t-tien-12m-160-ty-6-ty-n-2-thangmay-1ham-pr44913366"

def get_short_info(page, label):
    items = page.locator("div.re__pr-short-info-item")
    for i in range(items.count()):
        item = items.nth(i)
        title = item.locator("span.title").inner_text().strip()
        if label in title:
            value = item.locator("span.value").inner_text().strip()
            ext = item.locator("span.ext").inner_text().strip() if item.locator("span.ext").count() else None
            return value, ext
    return None, None

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto(URL, wait_until="domcontentloaded")

    gia, _ = get_short_info(page, "Khoảng giá")
    dien_tich, mat_tien_ext = get_short_info(page, "Diện tích")
    so_phong_ngu, _ = get_short_info(page, "Phòng ngủ")

    data = {
        "dia_diem": page.locator(".re__pr-short-description span").first.inner_text()
            if page.locator(".re__pr-short-description span").count() else None,
        "vi_tri": None,
        "giay_to_phap_ly": None,
        "loai_nha": None,
        "dien_tich": dien_tich,
        "mat_tien": mat_tien_ext.replace("Mặt tiền", "").strip() if mat_tien_ext else None,
        "tang": None,
        "huong_nha": None,
        "so_phong_ngu": so_phong_ngu,
        "tinh_trang_nha": None,
        "so_phong_tam": None,
        "gia": gia
    }

    print("==== DATA ====")
    for k, v in data.items():
        print(f"{k}: {v}")

    page.pause()
**Step 1**
```bash
playwright install chromium
```
**Step 2**
Mở chromium (login một lần duy nhất). Để lưu lịch sử trang tránh bắt là bot.
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    context = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=False,
        args=[
            "--disable-blink-features=AutomationControlled",
        ]
    )

    page = context.new_page()
    page.goto("https://accounts.google.com")

    input("👉 Login Google xong rồi nhấn Enter...")

    context.close()
```
**Step 3**
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    context = p.chromium.launch_persistent_context(
        user_data_dir="/home/thang/pw-chrome-profile",
        headless=True
    )

    page = context.new_page()
    page.goto("https://myaccount.google.com")

    print(page.title())
    # crawl ở đây

    context.close()
```
```text
NHÓM TƯƠNG TÁC – GÕ, CLICK NHƯ NGƯỜI. Nhóm dùng hàng ngày
```

# .click()
**Ex**
```python
page.get_by_role("button", name="Login").click() # click nút login
```

# .fill() 
**Ex**
```python
page.get_by_role("textbox", name="Email").fill("test@gmail.com")
page.get_by_role("textbox", name="Password").fill("123456")
```

# .check()
**Ex**
```python
page.get_by_role("checkbox", name="Remember me").check()
```
& page.type() & page.press()
## search google
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()

    page.goto("https://www.google.com")
    page.wait_for_selector("textarea[name='q']")

    # Điền nội dung (xóa text cũ)
    page.fill("textarea[name='q']", "Playwright python")

    # Nhấn Enter
    page.press("textarea[name='q']", "Enter")

    page.wait_for_timeout(5000)
    browser.close()
```
- NHÓM LẤY DỮ LIỆU (SCRAPING). Crawl dữ liệu web


& locator.all_inner_texts() & locator.get_attribute()
## Lấy tiêu đề trang
```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()

    page.goto("https://example.com")

    # Lấy text thẻ h1
    title = page.text_content("h1")

    print("Tiêu đề:", title)

    browser.close()
```