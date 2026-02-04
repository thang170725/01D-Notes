- [sync\_playwright \& .launch()](#sync_playwright--launch)
- [.launch\_persistent\_context()](#launch_persistent_context)
- [.new\_page()](#new_page)
---
# sync_playwright & .launch()
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
# .new_page()
```bash
- Trong Playwright Python, new_page dùng để mở một tab (page) mới trong cùng một browser context.
```
**Khi nào thì dùng new_page?**
```bash
- Website mở link sang tab mới
- Test nhiều user / nhiều màn hình trong cùng session
- So sánh dữ liệu giữa 2 trang
- Popup / OAuth / Payment / External link
```
