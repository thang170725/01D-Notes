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
