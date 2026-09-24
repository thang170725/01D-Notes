- [Ngrok Introduction (tạo một đường hầm cho người dùng trên internet truy cập được vào mạng local)](#ngrok-introduction-tạo-một-đường-hầm-cho-người-dùng-trên-internet-truy-cập-được-vào-mạng-local)
- [Ask](#ask)
  - [Trường hợp tạo đường hầm cho người dùng test website chạy trên mạng local](#trường-hợp-tạo-đường-hầm-cho-người-dùng-test-website-chạy-trên-mạng-local)
---
# Ngrok Introduction (tạo một đường hầm cho người dùng trên internet truy cập được vào mạng local)
# Ask
## Trường hợp tạo đường hầm cho người dùng test website chạy trên mạng local
```bash
Có một web phải chạy 4 terminal:
   - fe chạy port 5173
   - be chạy 3651 
   - đã dùng cors kết nối chạy bình thường 
```
```bash
Nhưng có một điểm rất quan trọng: nếu frontend của bạn chạy 5173 và backend chạy 3651, thì chỉ ngrok port 5173 chưa chắc backend tự truy cập được. Có 2 trường hợp.
   Trường hợp 1: FE gọi BE bằng localhost:3651
      Ví dụ FE của bạn đang có: axios.get("http://localhost:3651/api/recipes")

      Bạn tạo: ngrok http 5173

      Bạn gửi bạn mình: https://abc123.ngrok-free.app

      Bạn ấy mở được frontend, nhưng khi FE chạy trên máy bạn ấy, JavaScript sẽ gọi: http://localhost:3651/api/recipes
         ⚠️ localhost lúc này là máy của bạn ấy, không phải máy bạn. => Không gọi được backend của bạn.

   Trường hợp 2: FE gọi BE qua cùng domain ngrok
      Internet -> https://abc123.ngrok-free.app -> Frontend :5173 -> Backend :3651 # Nhưng cần cấu hình để request /api/... từ FE được proxy sang BE.

      Ví dụ Vite:
         vite.config.js:
            export default {
              server: {
                port: 5173,
                proxy: {
                  "/api": {
                    target: "http://localhost:3651",
                    changeOrigin: true,
                  },
                },
              },
            }

         Frontend gọi: axios.get("/api/recipes") không gọi axios.get("http://localhost:3651/api/recipes")

         Khi bạn chạy: ngrok http 5173 người bạn truy cập https://abc123.ngrok-free.app

         Flow sẽ là:
            Bạn của bạn
                  │
                  │ https://abc123.ngrok-free.app
                  ▼
               ngrok
                  │
                  ▼
            localhost:5173  (FE)
                  │
                  │ /api/recipes
                  ▼
            localhost:3651  (BE)

         Và BE không cần mở một ngrok riêng.

         Tuy nhiên có một vấn đề khác Nếu backend của bạn có những thứ như:
            - WebSocket
            - OAuth callback
            - file upload
            - API endpoint
            - SSE
         -> thì cần xem cấu hình cụ thể. Đặc biệt nếu frontend hiện tại đang cấu hình:
            VITE_API_URL=http://localhost:3651 -> thì chỉ ngrok FE là chưa đủ.

         Bạn nên chuyển sang: VITE_API_URL=/api rồi để Vite proxy /api → http://localhost:3651
            Với setup của bạn. Bạn nói hiện tại có:
               - Terminal 1: FE :5173
               - Terminal 2: BE :3651
               - ...

Nếu mục tiêu đơn giản là: "Tôi gửi một link cho bạn tôi, bạn ấy mở link và dùng toàn bộ web như đang chạy local."
   thì kiến trúc nên là:
      INTERNET -> https://xxxxx.ngrok-free.app -> ngrok -> FE :5173 -> /api/... request -> BE :3651
   => Thường chỉ cần ngrok 5173, miễn là FE proxy API sang BE 3651.

Nếu bạn đưa mình vite.config.* + file .env của FE + đoạn code cấu hình axios/fetch gọi BE, mình có thể chỉ chính xác cần sửa những dòng nào để web của bạn chạy qua đúng một link ngrok.
```