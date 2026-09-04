- [Kiểm tra xem cổng có bị ai chiếm không](#kiểm-tra-xem-cổng-có-bị-ai-chiếm-không)
- [Xem PID đó là chương trình gì](#xem-pid-đó-là-chương-trình-gì)
- [Kiểm tra các dịch vụ](#kiểm-tra-các-dịch-vụ)
- [Stop-Service](#stop-service)
- [net stop](#net-stop)
- [netstat -ano | findstr](#netstat--ano--findstr)
- [taskkill /PID 1234 /F](#taskkill-pid-1234-f)
- [Start-Service | net start](#start-service--net-start)
- [Get-Service](#get-service)
- [Get-NetIPConfiguration (xem IP, Gateway, DNS)](#get-netipconfiguration-xem-ip-gateway-dns)
- [Get-NetIPAddress -AddressFamily IPv4](#get-netipaddress--addressfamily-ipv4)
- [Get-NetRoute -AddressFamily IPv4](#get-netroute--addressfamily-ipv4)
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
# Get-NetIPConfiguration (xem IP, Gateway, DNS)
```bash
Mục đích là dùng 3 thông tin này để xác định máy bạn đang nằm ở đâu trong hạ tầng mạng
```
**Syn**
```bash
PS C:\Users\thang.ld> Get-NetIPConfiguration
# InterfaceAlias       : Ethernet
# InterfaceIndex       : 5
# InterfaceDescription : Realtek PCIe GbE Family Controller
# NetProfile.Name      : insmart.com.vn
# IPv4Address          : 192.168.9.75
# IPv6DefaultGateway   :
# IPv4DefaultGateway   : 192.168.9.1
# DNSServer            : 192.168.1.2
#                        192.168.1.3
#                        172.16.14.2
```
# Get-NetIPAddress -AddressFamily IPv4
**Ex**
```bash
PS C:\Users\thang.ld> Get-NetIPAddress -AddressFamily IPv4


IPAddress         : 192.168.9.75
InterfaceIndex    : 5
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Dhcp
SuffixOrigin      : Dhcp
AddressState      : Preferred
ValidLifetime     : 7.22:33:08
PreferredLifetime : 7.22:33:08
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 127.0.0.1
InterfaceIndex    : 1
InterfaceAlias    : Loopback Pseudo-Interface 1
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 8
PrefixOrigin      : WellKnown
SuffixOrigin      : WellKnown
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore
```
# Get-NetRoute -AddressFamily IPv4
**Ex**
```bash
PS C:\Users\thang.ld> Get-NetRoute -AddressFamily IPv4
# ifIndex DestinationPrefix                              NextHop                                  RouteMetric ifMetric PolicyStore
# ------- -----------------                              -------                                  ----------- -------- -----------
# 5       255.255.255.255/32                             0.0.0.0                                          256 25       ActiveStore
# 1       255.255.255.255/32                             0.0.0.0                                          256 75       ActiveStore
# 5       224.0.0.0/4                                    0.0.0.0                                          256 25       ActiveStore
# 1       224.0.0.0/4                                    0.0.0.0                                          256 75       ActiveStore
# 5       192.168.9.255/32                               0.0.0.0                                          256 25       ActiveStore
# 5       192.168.9.75/32                                0.0.0.0                                          256 25       ActiveStore
# 5       192.168.9.0/24                                 0.0.0.0                                          256 25       ActiveStore
# 1       127.255.255.255/32                             0.0.0.0                                          256 75       ActiveStore
# 1       127.0.0.1/32                                   0.0.0.0                                          256 75       ActiveStore
# 1       127.0.0.0/8                                    0.0.0.0                                          256 75       ActiveStore
# 5       0.0.0.0/0                                      192.168.9.1                                        0 25       ActiveStore
```