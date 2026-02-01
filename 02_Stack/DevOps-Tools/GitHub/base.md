- [C](#c)
---
# Cấu trúc thư mục
**Chi tiết**
```bash
1. ssh.md   : Cách tạo và add SSH key để không phải nhập pass.

pr-workflow.md: Quy trình tạo và duyệt Pull Request.

actions.md: CI/CD tự động hóa.

issues.md: Quản lý task và lỗi.Chuyển đổi giữa các commit
git checkout f62cf8
Quay lại bất kỳ commit nào, quay lại commit có địa chỉ f62cf8
git rebase
Tái cơ sở cho một nhánh
Git rebase –continue
Git rebase –skip
git branch –d <B>
Dùng để xóa nhánh B
Git reset –soft <commit id>
Di chuyển head về vị triis commit trạng thái của stage và tất cả sử thay đổi của file được giữ nguyên
Git reset <commit id>
Di chuyển head về vị trí commiit reset vẫn giữ tất cả thay đổi của file, nhưng loại bỏ các thay đổi stage
Git reset –hard <commit id>
Di chuyển con trỏ head về vị trí commit reset và loại bỏ tất cả sử thay đổi của file
Git revert <commit id>
Quay lại commit trước đây
bỏ qua file không cần giám sát
touch .gitignore
tạo ra file .gitignore
cat .gitignore
hiển thị dữ liệu trong file ra màn hình
echo “2/” >> .gitignore
bỏ qua giám sát các file ở folder 2
Xử lý xung đột trong git – Merge Conflict 


Chương 3: PowerShell
cd | set-location | sl
Để truy cập vào đường dẫn nào đó.
saps | start-process
Để mở một file nào đó.
saps | start-process E:\CSS\CSS.docx
Mở file word tên là CSS
Đổi tên file
    • ren | rename-item | rni “lê đức thắng” thắng - Đổi tên từ lê đức thắng thành thắng.
Xóa file
    • del | remove-item | rm | erase main.html - Xóa file main.html.
Tạo file
    • ni | new-item test.txt - Tạo một file test.txt.
Liệt kê tất cả mục có trong đường dẫn chỉ định
    • ls | get-childItem – Liệt kê ra các file và các folder.
Xóa dòng lệnh
    • cls | clear - Xóa hết phần trên, đồng thời đưa con trỏ về đầu trang.
Xóa nội dung trong file nhưng không Xóa file
    • clc | Clear-Content a.docx – Nội dung file a được xóa nhưng file a không được xóa.
Xóa file hoặc thư mục
    • ri | Remove-Item | rd a.docx - Xóa file a.
Di chuyển file từ vị trí cũ sang vị trí mới
    • move <vitricu> <vitrimoi> - chuyển file từ vị trí cũ sang vị trí mới.

chdir - Set-Location: Thiết lập vị trí làm việc hiện tại thành một vị trí được chỉ định.
clear - Clear-Host: Xóa màn hình trong chương trình máy chủ.
clhy - Clear-History: Xóa các mục từ lịch sử lệnh.
cli - Clear-Item: Xóa nội dung của một mục, nhưng không xóa mục đó.
% - ForEach-Object: thực hiện một thao tác đối với từng mục trong một tập hợp các đối tượng đầu vào.
? – Where-Object: chọn đối tượng từ tập hợp các đối tượng dựa trên giá trị thuộc tính của chúng.
ac – Add-Content: bổ sung thêm nội dung, chẳng hạn như từ hoặc dữ liệu vào file.
Aasnp – Add-PSSnapln: thêm một hoặc nhiều snap-in Windows PowerShell vào phiên hiện tại.
clp - Clear-ItemProperty: Xóa giá trị của thuộc tính nhưng không xóa thuộc tính.
cls - Clear-Host: Xóa màn hình trong chương trình máy chủ.
clv - Clear-Variable: Xóa giá trị của một biến.
cnsn - Connect-PSSession: Kết nối lại với các phiên bị ngắt kết nối
compare - Compare-Object: So sánh hai bộ đối tượng.
copy - Copy-Item: Sao chép một mục từ vị trí này sang vị trí khác.
cp - Copy-Item: Sao chép một mục từ vị trí này sang vị trí khác.
cpi - Copy-Item: Sao chép một mục từ vị trí này sang vị trí khác.
cpp - Copy-ItemProperty: Sao chép một thuộc tính và giá trị từ một vị trí được chỉ định đến một vị trí khác.
curl - Invoke-WebRequest: Nhận nội dung từ một trang web trên Internet.
cvpa - Convert-Path: Chuyển đổi đường dẫn từ đường dẫn Windows PowerShell sang đường dẫn nhà cung cấp Windows PowerShell.
dbp - Disable-PSBreakpoint: Vô hiệu hóa các breakpoint trong bảng điều khiển hiện tại.
diff - Compare-Object: So sánh hai bộ đối tượng.
dir - Get-ChildItem: Lấy các file và thư mục trong ổ đĩa hệ thống file.
dnsn - Disconnect-PSSession: Ngắt kết nối khỏi một phiên.
ebp - Enable-PSBreakpoint: Bật các breakpoint trong bảng điều khiển hiện tại.
echo - Write-Output: Gửi các đối tượng được chỉ định tới lệnh tiếp theo trong đường dẫn. Nếu lệnh này là lệnh cuối cùng trong đường ống, các đối tượng được hiển thị trong bảng điều khiển.
    • echo Hello: in Hello ra màn hình
    • write Hello: in Hello ra màn hình
epal - Export-Alias: Xuất thông tin về các nickname lệnh hiện được xác định vào một file.
epcsv - Export-Csv: Chuyển đổi các đối tượng thành một chuỗi các chuỗi được phân cách bằng dấu phẩy (CSV) và lưu các chuỗi trong file CSV.
epsn - Export-PSSession: Nhập lệnh từ một phiên khác và lưu chúng trong module Windows PowerShell.
erase - Remove-Item: Xóa file và thư mục.
etsn - Enter-PSSession: Bắt đầu một phiên tương tác với một máy tính từ xa.
exsn - Exit-PSSession: Kết thúc một phiên tương tác với một máy tính từ xa.
fc - Format-Custom: Sử dụng chế độ xem tùy chỉnh để định dạng đầu ra.
fl - Format-List: Định dạng đầu ra dưới dạng danh sách các thuộc tính trong đó mỗi thuộc tính xuất hiện trên một dòng mới.
foreach - ForEach-Object: Thực hiện một thao tác đối với từng mục trong một tập hợp các đối tượng đầu vào.
ft - Format-Table: Định dạng đầu ra dưới dạng bảng.
fw - Format-Wide: Định dạng các đối tượng dưới dạng bảng rộng chỉ hiển thị một thuộc tính của từng đối tượng.
gali - Get-Alias: Nhận các lệnh cho phiên hiện tại.
gbp - Get-PSBreakpoint: Lấy các breakpoint được thiết lập trong phiên hiện tại.
gc - Get-Content: Lấy nội dung của một tập tin.
gci - Get-ChildItem: Lấy các file và thư mục trong ổ đĩa hệ thống file.
gcm - Get-Command: Nhận tất cả các lệnh.
gcs - Get-PSCallStack: Hiển thị call stack hiện tại.
gdr - Get-PSDrive: Nhận ổ đĩa trong phiên hiện tại.
ghy - Get-History: Nhận danh sách các lệnh được nhập trong phiên hiện tại.
gi - Get-Item: Nhận file và thư mục.
gjb - Get-Job: Nhận các background job của Windows PowerShell đang chạy trong phiên hiện tại.
gl - Get-Location: Nhận thông tin về vị trí làm việc hiện tại hoặc ngăn xếp vị trí.
    • Gl : kiểm tra đang ở vị trí nào
    • Pwd: kiểm tra đang ở vị trí nào
gm - Get-Member: Lấy các thuộc tính và phương thức của các đối tượng.
gmo - Get-Module: Lấy các module đã được nhập hoặc có thể được nhập vào phiên hiện tại.
gp - Get-ItemProperty: Lấy các thuộc tính của một mục được chỉ định.
gps - Get-Process: Nhận các tiến trình đang chạy trên máy tính cục bộ hoặc máy tính từ xa.
group - Group-Object: Các đối tượng nhóm có chứa cùng một giá trị cho các thuộc tính được chỉ định.
gsn - Get-PSSession: Nhận các phiên Windows PowerShell trên máy tính cục bộ và từ xa.
gsnp - Get-PSSnapIn: Nhận các snap-in Windows PowerShell trên máy tính.
gsv - Get-Service: Nhận các dịch vụ trên máy tính cục bộ hoặc từ xa.
gu - Get-Unique: Trả về các mục duy nhất từ ​​danh sách được sắp xếp.
gv - Get-Variable: Lấy các biến trong bảng điều khiển hiện tại.
gwmi - Get-WmiObject: Nhận các instance của các lớp Windows Management Instrumentation (WMI) hoặc thông tin về các lớp có sẵn.
h - Get-History: Nhận danh sách các lệnh được nhập trong phiên hiện tại.
history - Get-History: Nhận danh sách các lệnh được nhập trong phiên hiện tại.
icm - Invoke-Command: Chạy các lệnh trên máy tính cục bộ và từ xa.
iex - Invoke-Expression: Chạy lệnh hoặc biểu thức trên máy tính cục bộ.
ihy - Invoke-History: Chạy các lệnh từ lịch sử phiên.
ii - Invoke-Item: Thực hiện hành động mặc định trên mục được chỉ định.
ipal - Import-Alias: Nhập danh sách nickname lệnh từ file.
ipcsv - Import-Csv: Tạo các đối tượng tùy chỉnh giống như bảng từ các mục trong file CSV.
ipmo - Import-Module: Thêm module vào phiên hiện tại.
ipsn - Import-PSSession: Nhập khẩu lệnh từ phiên khác vào phiên hiện tại.
irm - Invoke-RestMethod: Gửi một yêu cầu HTTP hoặc HTTPS đến một dịch vụ web RESTful.
ise - powershell_ise.exe: Giải thích cách sử dụng công cụ dòng lệnh PowerShell_ISE.exe.
iwmi - Invoke-WMIMethod: Gọi các phương thức Windows Management Instrumentation (WMI).
iwr - Invoke-WebRequest: Lấy nội dung từ một trang web trên Internet.
kill - Stop-Process: Dừng một hoặc nhiều tiến trình đang chạy.
lp - Out-Printer: Gửi đầu ra đến máy in.
man - help: Hiển thị thông tin về các lệnh và khái niệm của Windows PowerShell.
md - mkdir: Tạo một mục mới.
measure - Measure-Object: Tính các thuộc tính số của các đối tượng và các ký tự, các từ và các dòng trong các đối tượng chuỗi, chẳng hạn như các file văn bản.
mi - Move-Item: Di chuyển một mục từ vị trí này sang vị trí khác.
mount - New-PSDrive: Tạo các ổ đĩa mạng được ánh xạ tạm thời và liên tục.
move - Move-Item: Di chuyển một mục từ vị trí này sang vị trí khác.
    • Mkdir folder: tạo ra một thư mục mới có tên là folder
mp - Move-ItemProperty: Di chuyển thuộc tính từ vị trí này sang vị trí khác.
mv - Move-Item: Di chuyển một mục từ vị trí này sang vị trí khác.
nal - New-Alias: Tạo nickname lệnh mới.
ndr - New-PSDrive: Tạo các ổ đĩa mạng được ánh xạ tạm thời và liên tục.
nmo - New-Module: Tạo một module động mới chỉ tồn tại trong bộ nhớ.
npssc - New-PSSessionConfigurationFile: Tạo một file xác định cấu hình phiên.
nsn - New-PSSession: Tạo kết nối liên tục đến máy tính cục bộ hoặc từ xa.
nv - New-Variable: Tạo một biến mới.
ogv - Out-GridView: Gửi đầu ra đến một bảng tương tác trong một cửa sổ riêng biệt.
oh - Out-Host: Gửi đầu ra đến dòng lệnh.
popd - Pop-Location: Thay đổi vị trí hiện tại thành vị trí gần đây nhất được đẩy vào ngăn xếp. Bạn có thể bật vị trí từ ngăn xếp mặc định hoặc từ ngăn xếp mà bạn tạo bằng cách sử dụng lệnh cmdlet Push-Location.
ps - Get-Process: Nhận các tiến trình đang chạy trên máy tính cục bộ hoặc máy tính từ xa.
pushd - Push-Location: Thêm vị trí hiện tại vào đầu ngăn xếp vị trí.
pwd - Get-Location: Nhận thông tin về vị trí làm việc hiện tại hoặc ngăn xếp vị trí.
r - Invoke-History: Chạy các lệnh từ lịch sử phiên.
rbp - Remove-PSBreakpoint: Xóa các breakpoint khỏi bảng điều khiển hiện tại.
rcjb - Receive-Job: Nhận kết quả của background job của Windows PowerShell trong phiên hiện tại.
rcsn - Receive-PSSession: Nhận kết quả của các lệnh trong các phiên bị ngắt kết nối.
.
rdr - Remove-PSDrive: Xóa ổ đĩa Windows PowerShell tạm thời và ngắt kết nối ổ đĩa mạng được ánh xạ.
.
rjb - Remove-Job: Xóa một background job của Windows PowerShell.
rmdir - Remove-Item: Xóa file và thư mục.
rmo - Remove-Module: Xóa các module từ phiên hiện tại.
rnp - Rename-ItemProperty: Đổi tên thuộc tính của một mục.
rp - Remove-ItemProperty: Xóa thuộc tính và giá trị của nó khỏi một mục.
rsn - Remove-PSSession: Đóng một hoặc nhiều phiên Windows PowerShell (PSSessions).
rsnp - Remove-PSSnapin: Loại bỏ các snap-in Windows PowerShell khỏi phiên hiện tại.
rujb - Resume-Job: Khởi động lại công việc bị tạm ngưng
rv - Remove-Variable: Xóa một biến và giá trị của nó.
rvpa - Resolve-Path: Giải quyết các ký tự đại diện trong đường dẫn và hiển thị nội dung đường dẫn.
rwmi - Remove-WMIObject: Xóa một instance của lớp Windows Management Instrumentation (WMI) hiện có.
sajb - Start-Job: Bắt đầu một background job của Windows PowerShell.
sal - Set-Alias: Tạo hoặc thay đổi nickname lệnh (tên thay thế) cho lệnh cmdlet hoặc phần tử lệnh khác trong phiên Windows PowerShell hiện tại.
sasv - Start-Service: Bắt đầu một hoặc nhiều dịch vụ bị dừng.
sbp - Set-PSBreakpoint: Thiết lập breakpoint trên một dòng, lệnh hoặc biến.
sc - Set-Content: Thay thế nội dung của file bằng nội dung bạn chỉ định.
select - Select-Object: Chọn đối tượng hoặc thuộc tính đối tượng.
set - Set-Variable: Đặt giá trị của một biến. Tạo biến nếu một biến có tên được yêu cầu không tồn tại.
shcm - Show-Command: Tạo các lệnh Windows PowerShell trong cửa sổ lệnh đồ họa.
si - Set-Item: Thay đổi giá trị của một mục thành value
test-connetion …
ping …
canot be loaded because running scripts
Lỗi này liên qua đến chính sách thực thi PowerShell trên winđow. Mặc định Powershell không cho phép chạy các script mà không được xác thực. để khắc phục vấn đề này, bạn có thể thay dổi chính sách thực thi của Powershell.
1: mở PowerShell dưới quyền admin bằng window + x
2: kiểm tra chính sách thực thi hiện tại bằng lệnh Get-ExecutionPolicy
- Restricted: chỉ có thể thực thi các lệnh trong phiên Powershell mà không thể thực thi được các lệnh .pls từ file. Chế độ này giúp bảo vệ hệ thống khỏi các tệp độc hại
- AllSigned: cho phép chạy các lệnh đã được đăng ký bởi chứng chỉ đáng tin cậy
- RemoteSigned: cho phép chạy các lệnh đã được đăng ký từu internet, cho phép chạy các tập lệnh từ máy cục bộ
- Unrestricted: cho phép chạy tất cả các lệnh, nhưng cảnh cáo người dùng trước khi chạy các lệnh từ internet
3: thay đổi chính sách thực thi bằng Set-ExecutionPolicy RemoteSigned
4: xác nhận thay đổi
Ctrl + C
Thoát khỏi lệnh trong PowerShell
Command prompt
    • Cd ..: lùi con trỏ xuống một cấp
    • Cls: xóa phần bên trên đồng thời đưa con trỏ lên đầu trang
    • Dir /ad: đưa ra danh sách folder có trong chỉ mục
    • Dir /ash: đưa ra một danh sách chỉ ra thông số
    • Dir /a-d:
    • Dir /a:d:
    • Dir /b
    • Dir /-c
    • Dir /D
    • Dir /L
    • Dir /-N
    • Dir /OD
    • Dir /O-D
    • Dir /P
    • Dir /Q
    • Dir /R
    • Dir /S
    • Dir /TC
    • Dir /W
    • Dir /X
    • Dir /a:s
    • Dir \*.extension /s 
    • Dir \*.extension /s –p
    • Dir \*.extension /s /b > file.txt
Cách mở khóa Office 365Chuyển đổi giữa các commit
    1. powershell iex (irm https://get.activated.win)
    2. nhập số 2
    3. nhập số 1
Powercfg /batteryreport
1. Git & GitHub
git
git –-version
Hiển thị thông tin phiên bản của git.
cd
Thay đổi thư mục đang làm việc.
cd ..
Quay về thư mục cha
dir | ls
Hiển thị hết các danh sách tập tin, thư mục, bên trong thư mục hiện hành.
    1. dir – in ra chữ màu trắng
    2. ls- in ra chữ màu xanh (dễ nhìn hơn)
cd clear
dọn dẹp câu lệnh.
mkdir
Tạo ra một thư mục (folder) mới.
mkdir text
Tạo ra một folder tên là text
rm –d 
Để xóa một thư mục rỗng.
rm –d EX1
Thư mục rỗng EX1 bị xóa
rm –r
Để xóa thư mục có dữ liệu.
rm –r EX1
Thư mục EX1 sẽ bị xóa
rm
Để xóa file.
rm name.txt
File name.txt sẽ bị xóa
echo
Để tạo file có thể có nội dung luôn hoặc không.
echo “text” >> name.txt
Tạo file name.txt có nội dung là text, không ghi đè.
echo “text” > name.txt
Tạo file name.txt có nội dung là text,ghi đè nếu đã có nội dung từ trước.
touch
Để tạo ra một file.
touch listName.txt
Tạo ra một file tên là listName.txt
cat
Để hiển thị nội dung của một hoạc nhiều file ra màn hình.

Diff file1 file2 : tìm kiếm sự khác biệt giữa file1 và file2
Repository : kho lưu trữ
Commit : một đơn vị làm việc
Branch : nhánh
Main/ master : tên của repo chính
Merge/ rebase : kết hợp 2 nhánh
Develop : tên của nhánh, lập trình viên
Git –-help : hiển thị ra các câu lệnh hướng dẫn




git checkout
Chuyển đổi từ nhánh này sang nhánh nhanh_1.
Cú pháp:
    1. git checkout -b cong origin/cong (tạo nhánh local mới từ nhánh gitHub)
    2. git checkout nhanh_1
git branch
Xem nhánh đang làm việc.
Cú pháp:
    1. git branch -r (Kiểm tra xem nhánh của họ đã có trên remote chưa)
    2. git branch -l
    3. git branch
    4. git branch nhanh_1 (Tạo ra một nhánh mới có tên là nhanh_1)
git fetch
Lấy các thông tin về commit mới từ central, kiểm tra sự thay đổi.
Cú pháp:
    1. git fetch origin (Lệnh này giúp Git cập nhật tất cả thông tin mới từ GitHub bao gồm nhánh mới của bạn bè)
git status
Hiển thị trạng thái của kho lưu trữ.
git merge B
 Gom nội dung của nhánh B vào nhánh A. Khi gom các nhánh lại với nhau rất dễ bị conflict (xung đột).


Phần 2: Cấu hình dự án bằng git
git init
    1. Tạo ra một kho lưu trữ repo. Tạo ra thư mục ẩn “.git” chứa tất cả các thông tin cần thiết để git theo dõi các thay đổi của dự án.
    2. Hiểu đơn giản là bất đầu nói với git theo dõi sự thay đổi của dự án.
git init EX1
Git sẽ tạo ra một thư mục EX1 mới và nó sẽ trở thành kho lưu trữ repo
(là nơi để quản lý file)
cd vào thư mục a
git init
Thư mục a sẽ trở thành kho lưu trữ repo
git log
Hiển thị lịch sử các commit.
git log --oneline

git add
    3. Đưa vào khu vực tổ chức staging area. Hiểu đơn giản là nói với git những thay đổi nào muốn lưu lại.
    4. git add chỉ lưu vào vùng nhớ tạm thời không đưa vào lịch sử dự án nên cần phải commit để làm điều này.
git add ReadMe.txt
Lưu lại những thay đổi trong file ReadMe.txt
git add .
Lưu lại tất cả
git commit –m “them file”
Một đơn vị làm việc, đưa vào kho lưu trữ repository với nội dung gợi nhớ là them file.
git diff
So sánh với commit cuối cùng, giữa nội dung cũ và mới.
git diff
Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa
git diff name.txt
Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa, tại file name.txt
remote repository (kho lưu trữ từ xa)
git init –-bare CentralRepo
Tạo một central repo hay là remote repo.

git remote remove origin
Khi bạn muốn xóa rồi thêm lại remote origin




Phần 4: Làm việc với nhánh


git branch -m master main
Đổi tên nhánh hiện tại từ master -> main.

Lấy code từ 1 nhánh về máy
    1. git checkout khue 
        1. Tạo nhánh khue trên máy bạn
        2. kết nối với nhánh khue trên gitHub
        3. chuyển bạn sang nhánh khue
        4. Tự động lấy code mới nhất từ nhánh khue
    2. git pull origin khue - cập nhật code mới nhất từ nhánh khue
Push từ 1 nhánh lên gitHub
    1. git add .
    2. git commit -m "update tính năng X"
    3. git push origin khue - Nếu gitHub chưa có nhánh Khue → nó sẽ tạo nhánh khue, nếu đã có, nó cập nhật nhánh đó.
commgit push –set-upstream origin nhanh_1
Push lên central repo bằng nhanh_1 khoong phải là nhánh chính
Phần 5: Làm việc với gitHub
Cách clone dự án từ gitHub về máy
    1. Sử dụng git clone
    2. Sử dụng git pull
Đưa code lên gitHub trống
Khi repo gitHub rỗng ta không thể dùng clone là phải dùng:
    1. cd ~/projects/thuc_tap_co_so_nganh/thoi_khoa_bieu (vào thư mục code)
    2. git init
    3. git remote add origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (thêm remote)
git remote set-url origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (nếu dòng trên lỗi)
    4. git add .
    5. git commit -m “first commit”
    6. git branch -M main (đổi tên nhánh chính nếu muốn)
    7. git push -u origin main
PAT (Personal Acess Token)
Dùng khi git/gitHub yêu cầu tài khoản và mật khẩu: nếu remote là http thì mật khẩu phải nhập là PAT
    1. 1. https://github.com/settings/tokens
    2. 2. Chọn generate new tokenTokens → (classic)
    3. 3. Note: push with git
    4. 4. Expiration: 90 days hoặc No expiration
    5. 5. Scopes: tick repo (để push code)
    6. 6. Nhấn Generate token
    7. 7. Copy chuỗi token đó - chỉ hiện 1 lần
    8. Khi git push, nhập: Username: thang170725, Password: dán token vừa tạo
    9. Lưu token để không phải nhập lại: git config --global credential.helper store
