- [Kiểm tra xem cổng có bị ai chiếm không](#kiểm-tra-xem-cổng-có-bị-ai-chiếm-không)
- [Xem PID đó là chương trình gì](#xem-pid-đó-là-chương-trình-gì)
- [Kiểm tra các dịch vụ](#kiểm-tra-các-dịch-vụ)
- [Stop-Service](#stop-service)
- [net stop](#net-stop)
- [netstat -ano | findstr](#netstat--ano--findstr)
- [taskkill /PID 1234 /F](#taskkill-pid-1234-f)
- [Start-Service | net start](#start-service--net-start)
- [Get-Service](#get-service)
---
# Kiểm tra xem cổng có bị ai chiếm không
```bash
netstat -ano | findstr :3306
```
**Ex**
```bash
PS D:\workspace\dev-note> netstat -ano | findstr :3306
  TCP    0.0.0.0:3306           0.0.0.0:0              LISTENING       10360
  TCP    0.0.0.0:33060          0.0.0.0:0              LISTENING       10360
  TCP    [::]:3306              [::]:0                 LISTENING       10360
  TCP    [::]:33060             [::]:0                 LISTENING       10360
```
# Xem PID đó là chương trình gì
```bash
tasklist /FI "PID eq 1234"
```
# Kiểm tra các dịch vụ
```bash
Get-Service *mysql* | sc query type= service | findstr /I mysql
```
# Stop-Service 
# net stop
# netstat -ano | findstr 
# taskkill /PID 1234 /F
# Start-Service | net start
# Get-Service