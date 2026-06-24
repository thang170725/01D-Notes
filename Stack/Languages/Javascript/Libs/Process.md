- [L.map() \& .setView() \& L.titleLayer()](#lmap--setview--ltitlelayer)
- [L.marker() \& .addTo \& .bindPopup()](#lmarker--addto--bindpopup)
- [L.polyline() \& .distanceTo()](#lpolyline--distanceto)
- [axios](#axios)
---
- Leaflet là thư viện nhẹ, miễn phí, rất phổ biến, cực phù hợp cho người mới.
- Leaflet làm được gì?
  + Hiển thị bản đồ
  + Zoom / pan
  + Thêm marker, line, polygon
  + Xử lý click, drag
  + Kết hợp tốt với Python backend sau này

# L.map() & .setView() & L.titleLayer()
```bash
- L.map('map') → Gắn bản đồ vào <div id="map">
- .setView([lat, lng], zoom) → Vị trí ban đầu + mức zoom
- L.tileLayer(...) → Nguồn tile (ở đây là OpenStreetMap)
```
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Bản đồ đầu tiên</title>

  <!-- Leaflet CSS -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet/dist/leaflet.css"
  />

  <style>
    #map {
      height: 400px;
    }
  </style>
</head>
<body>

  <div id="map"></div>

  <!-- Leaflet JS -->
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

  <script>
    // Tạo bản đồ
    var map = L.map('map').setView([21.0285, 105.8542], 13);

    // Thêm tile layer (OpenStreetMap)
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 19
    }).addTo(map);
  </script>

</body>
</html>
```

# L.marker() & .addTo & .bindPopup()
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>Bản đồ đầu tiên</title>

    <!-- Leaflet CSS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

    <style>
        #map {
            height: 400px;
        }
    </style>
</head>

<body>

    <div id="map"></div>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

    <script>
        // Tạo bản đồ
        var map = L.map('map').setView([21.0285, 105.8542], 13);
        L.marker([21.0285, 105.8542])
            .addTo(map)
            .bindPopup("Xin chào Hà Nội");

        map.on('click', function (e) {
            console.log(e.latlng);
        });

        // Thêm tile layer (OpenStreetMap)
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            maxZoom: 19
        }).addTo(map);
    </script>

</body>

</html>
```

# L.polyline() & .distanceTo()
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>Bản đồ đầu tiên</title>

    <!-- Leaflet CSS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

    <style>
        #map {
            height: 400px;
        }
    </style>
</head>

<body>

    <div id="map"></div>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>

    <script>
        // Tạo bản đồ
        var map = L.map('map').setView([21.0285, 105.8542], 13);

        var latlngs = [
            [21.0285, 105.8542],
            [20.9843, 105.7840],
            [20.9500, 105.7500]
        ];

        var totalDistance = 0;
        for (var i = 0; i < latlngs.length - 1; i++) {
            var p1 = L.latLng(latlngs[i]);
            var p2 = L.latLng(latlngs[i + 1]);
            totalDistance += p1.distanceTo(p2);
        }
        console.log("Tổng khoảng cách: " + totalDistance + " mét");

        // Thêm tile layer (OpenStreetMap)
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            maxZoom: 19
        }).addTo(map);
    </script>

</body>

</html>
```
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Bản đồ tương tác hoàn chỉnh</title>

  <!-- Leaflet CSS -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet/dist/leaflet.css"
  />

  <style>
    #map {
      height: 600px;
    }
  </style>
</head>
<body>

<h2>Bản đồ tương tác: Marker + Polyline + Khoảng cách</h2>
<div id="map"></div>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<script>
  // 1. Tạo bản đồ, ban đầu nhìn Hà Nội
  var map = L.map('map').setView([21.0285, 105.8542], 13);

  // 2. Thêm tile layer từ OpenStreetMap
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19
  }).addTo(map);

  // 3. Danh sách marker (ban đầu rỗng)
  var markers = [];
  var latlngs = [];
  var polyline = null;

  // 4. Click bản đồ → thêm marker + cập nhật polyline
  map.on('click', function(e) {
    var marker = L.marker(e.latlng)
      .addTo(map)
      .bindPopup(
        "Lat: " + e.latlng.lat.toFixed(6) +
        "<br>Lng: " + e.latlng.lng.toFixed(6)
      )
      .openPopup();

    // Thêm vào danh sách
    markers.push(marker);
    latlngs.push(e.latlng);

    // Nếu có hơn 1 marker, vẽ polyline
    if (polyline) {
      map.removeLayer(polyline);
    }
    polyline = L.polyline(latlngs, {color: 'blue', weight: 4}).addTo(map);

    // Tính tổng quãng đường
    var totalDistance = 0;
    for (var i = 0; i < latlngs.length - 1; i++) {
      totalDistance += latlngs[i].distanceTo(latlngs[i+1]);
    }

    console.log("Tổng khoảng cách: " + totalDistance.toFixed(2) + " mét");

    // Hiển thị khoảng cách ở popup của marker cuối
    marker.bindPopup(
      "Lat: " + e.latlng.lat.toFixed(6) +
      "<br>Lng: " + e.latlng.lng.toFixed(6) +
      "<br>Tổng quãng đường: " + totalDistance.toFixed(2) + " m"
    ).openPopup();
  });
</script>

</body>
</html>
```

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Bản đồ Polygon + Marker</title>

  <!-- Leaflet CSS -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet/dist/leaflet.css"
  />

  <style>
    #map {
      height: 600px;
    }
  </style>
</head>
<body>

<h2>Bản đồ Polygon + Marker + Kiểm tra điểm</h2>
<div id="map"></div>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<!-- Turf.js cho kiểm tra point in polygon chính xác -->
<script src="https://cdn.jsdelivr.net/npm/@turf/turf@6/turf.min.js"></script>

<script>
  // 1. Tạo bản đồ, ban đầu nhìn Hà Nội
  var map = L.map('map').setView([21.0285, 105.8542], 15);

  // 2. Thêm tile layer từ OpenStreetMap
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19
  }).addTo(map);

  // 3. Vẽ Polygon (ví dụ: 1 vùng vuông nhỏ)
  var polygonLatLngs = [
    [21.0300, 105.8500],
    [21.0350, 105.8500],
    [21.0350, 105.8600],
    [21.0300, 105.8600]
  ];

  var polygon = L.polygon(polygonLatLngs, {
    color: 'green',
    fillColor: '#00FF00',
    fillOpacity: 0.3
  }).addTo(map);

  // 4. Click bản đồ → tạo marker + kiểm tra polygon
  map.on('click', function(e) {
    var lat = e.latlng.lat;
    var lng = e.latlng.lng;

    var marker = L.marker([lat, lng]).addTo(map);

    // Chuyển sang GeoJSON để kiểm tra
    var point = turf.point([lng, lat]);
    var polyCoords = polygonLatLngs.map(function(c) { return [c[1], c[0]]; }); // [lng, lat]
    polyCoords.push([polygonLatLngs[0][1], polygonLatLngs[0][0]]); // khép kín
    var poly = turf.polygon([polyCoords]);

    var inside = turf.booleanPointInPolygon(point, poly);

    // Hiển thị popup
    marker.bindPopup(
      "Lat: " + lat.toFixed(6) +
      "<br>Lng: " + lng.toFixed(6) +
      "<br>Kết quả: " + (inside ? "✅ Nằm trong vùng" : "❌ Ngoài vùng")
    ).openPopup();
  });
</script>

</body>
</html>

# axios
FetchAxiosCó sẵn trong browserPhải cài packageChuẩn Web APIThư viện bên thứ 3Nhẹ, không phụ thuộcNhiều tiện ích hơnPhải tự xử lý nhiều thứTự xử lý nhiều thứ giúp bạnHiện nay dùng rất phổ biếnVẫn rất phổ biến

Fetch là gì?
Là API có sẵn của JavaScript để gửi HTTP request.
const response = await fetch("/users");const data = await response.json();console.log(data);

Axios là gì?
Là thư viện giúp việc gọi API dễ hơn.
Cài:
npm install axios
Dùng:
import axios from "axios";const response = await axios.get("/users");console.log(response.data);

So sánh đơn giản
GET request
Fetch
const response = await fetch("/users");const data = await response.json();console.log(data);
Axios
const response = await axios.get("/users");console.log(response.data);
Axios ngắn hơn.

POST request
Fetch
await fetch("/users", {  method: "POST",  headers: {    "Content-Type": "application/json"  },  body: JSON.stringify({    name: "Thang"  })});

Axios
await axios.post("/users", {  name: "Thang"});
Axios tự:


JSON.stringify


Content-Type



Query Params
Fetch
const params = new URLSearchParams({  page: 1,  limit: 10});await fetch(`/users?${params}`);

Axios
await axios.get("/users", {  params: {    page: 1,    limit: 10  }});
Axios tiện hơn.

Xử lý lỗi
Đây là khác biệt quan trọng.
Fetch
const response = await fetch("/users");
Nếu API trả:
404
thì Fetch vẫn coi là thành công.
Bạn phải tự kiểm tra:
if (!response.ok) {  throw new Error("API Error");}

Axios
await axios.get("/users");
Nếu API trả:
404
Axios tự nhảy vào:
catch(error)
Ví dụ:
try {  await axios.get("/users");} catch (error) {  console.log(error.response.status);}

Interceptor (điểm mạnh lớn của Axios)
Giả sử mọi request đều cần token.
Axios
axios.interceptors.request.use((config) => {  const token = localStorage.getItem("token");  if (token) {    config.headers.Authorization = `Bearer ${token}`;  }  return config;});
Sau đó:
axios.get("/users");axios.get("/foods");axios.post("/meals");
Tự có token.

Fetch
Bạn phải tự viết wrapper giống cái JsonApi của bạn:
headers.Authorization = `Bearer ${token}`;
Thực chất bạn đang tự xây một phiên bản đơn giản của Axios.

Timeout
Axios
axios.get("/users", {  timeout: 5000});
5 giây không phản hồi là lỗi.

Fetch
Không có sẵn.
Phải dùng:
AbortController
khá dài dòng.

Upload file
Axios
const formData = new FormData();formData.append("image", file);await axios.post(  "/upload",  formData);
Rất đơn giản.

Fetch
Làm được nhưng thường phải xử lý nhiều thứ hơn.

Trong dự án React của bạn
Bạn đang có:
JsonApi()
bọc ngoài:
fetch()
Ví dụ:
await JsonApi("/users", {  params: {    page: 1  }});
Thực tế bạn đã thêm:


Authorization


params


error handling


JSON parsing


rồi.
Nghĩa là bạn đã giải quyết phần lớn nhược điểm của Fetch.

Khi nào dùng Fetch?
Mình thường dùng Fetch khi:


Dự án nhỏ


Không muốn cài thêm thư viện


React/Vite đơn giản


Có thể tự viết wrapper như bạn đang làm


Ví dụ:
JsonApi()FormDataApi()
là đủ.

Khi nào dùng Axios?
Thường dùng khi:


Dự án lớn


Nhiều API


Nhiều interceptor


Refresh token


Retry request


Timeout


Team nhiều người


Ví dụ:
api/ ├── axios.js ├── auth.js ├── meal.js ├── user.js
thì Axios khá tiện.

Kết luận
Với trình độ hiện tại và dự án React + FastAPI của bạn:


Hiểu kỹ fetch, Promise, async/await, URLSearchParams trước.


Wrapper JsonApi() hiện tại của bạn là hướng làm rất tốt.


Chưa cần chuyển sang Axios chỉ vì "nghe nói mạnh hơn".


Thực tế rất nhiều dự án production hiện nay vẫn dùng fetch + một wrapper giống hệt JsonApi của bạn. Khi bạn bắt đầu làm refresh token, interceptor phức tạp hoặc nhiều service hơn, lúc đó sẽ thấy rõ lợi ích của Axios.