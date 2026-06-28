- [link](#link)
- [a](#a)
- [source](#source)
- [Thẻ audio](#thẻ-audio)
- [video](#video)
---
# link
```bash
Liên kết file HTML với file bên ngoài. Thẻ Link không có thẻ đóng. Các viết tắt: link:css.
```
**Syn**
```bash
<link rel="stylesheet" href="Tester.css">

- rel
    + stylesheet    : giá trị được sử dụng phổ biến nhất. Liên kết với một biểu định kiểu bên ngoài.
    + icon          : Một tài nguyên biểu tượng. (<link rel="icon" href="./image/Hulk.jpg">)
    + preconnect    : 
- href  : gắn một liên kết là URL vào file html.
```
# a
```bash
Để tạo liên kết, điều hướng tới trang khác, … 
```
**Syn**
```bash
<a href="" title="tôi là thuộc tính title" target='_blank'></a>

- href  : Chỉ định URL của trang liên kết đến. Dùng “#” khi chưa cần gán link điều hướng cho thẻ.
- target: Chỉ định nơi mở tài liệu được liên kết. 
    + _blank: Tài liệu được mở ở của số khác.
    + _parent
    + _self
    + _top
```
# source 
Thẻ source được sử dụng để chỉ định tài nguyên đa phượng tiện cho các phần tử media ví dụ như video, audio, hình ảnh. Nó không có thẻ đóng 
# Thẻ audio 
Thẻ <audio> … </audio> sẽ định nghĩa đó là một file âm thanh, chẳng hạn như file nhạc hoặc môt luồng âm thanh khác
Có 3 định dạng được hỗ trợ bởi thẻ <audio>
    • MP3
    • Wav
    • Ogg
<audio src="partial-quran-recitation-from-juz-amma-344966.mp3" controls autoplay></audio>

# video
Thẻ <video> … </video> sẽ định nghĩa một video, nói cách khác nó sẽ nhúng một video vào trình duyệt.
Hiện nay, có 3 loại file video được hỗ trợ đó là: MP4, WebM, và Ogg.
Các trình duyệt hỗ trợ:
    • MP4: Chrome, Firefox, Opera, Safari, IE.
    • WebM: Chrome, Firefox, Opera.
    • Ogg: Chrome, Firefox, Opera.
Thẻ track
Thẻ <track>  được dùng để "chèn một bản phụ đề vào video". Nó không có thẻ đóng. File phụ đề phải có đuôi vtt
Cách tạo một tập tin phụ đề
- Bước 1: Tạo một tập tin phụ đề.
Mở notepad lên.
Bấm vào tab "File" rồi chọn "Save As".
Đặt tên cho tập tin xong rồi lưu lại.
(Lưu ý: Endcoding chọn UTF-8, và tập tin phải có phần đuôi là .vtt)

- Bước 2: Viết nội dung cho tập tin phụ đề.
Nội dung của một tập tin phụ đề phải được tắt đầu bằng cụm từ WEBVTT
Cách xác định thời điểm hiển thị phụ đề khá đơn giản, dưới đây là nội dung của tập tin phude.vtt
WEBVTT

00:00:00.500 --> 00:00:02.000
ý !?

00:00:02.000 --> 00:00:05.500
Con bươm bướm kìa !

00:00:06.000 --> 00:00:08.000
Nó đẹp quá ba mẹ ơi =))

00:00:09.000 --> 00:00:10.000
Thế éo nào!? @_@
Ví dụ:
<video controls style="width:100%">
    <source src="../file/bunny.mp4">
    <track src="../file/phude.vtt" default>
</video>
Chúng ta cũng có thể sử dụng kết hợp với các thẻ <i>, <u>, <b> để trang trí cho phụ đề.
Ví dụ, dưới đây là nội dung của tập tin phude2.vtt
WEBVTT

00:00:00.500 --> 00:00:02.000
ý !?

00:00:02.000 --> 00:00:05.500
Con <i><b><u>bươm bướm</u></b></i> kìa !

00:00:06.000 --> 00:00:08.000
<u>Nó đẹp quá ba mẹ ơi =))</u>

00:00:09.000 --> 00:00:10.000
Thế éo nào!? @_@
Ví dụ:
<video controls style="width:100%">
    <source src="../file/bunny.mp4">
    <track src="../file/phude2.vtt" default>
</video>
