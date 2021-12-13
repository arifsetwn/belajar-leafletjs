# 2. Web Map Pertama

## 2.1 Setup HTML

Untuk memulai pembuatan web map, silakan buat file dengan nama `index.html` dengan isian sebagai berikut

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basic Map</title>
</head>
<body>
  
</body>
</html>
```

kode diatas merupakan struktur dasar `HTML`, tidak ada yang perlu dijelaskan lebih lanjut 😄



## 2.2 Leaflet JS

Untuk menambahkan library leafletjs kita perlu meng-include 2 file yaitu `CSS` dan `Javascript`

### 2.2.1 CSS

Tambahkan kode berikut diantara `<head>`

```
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/>
```

### 2.2.2 Javascript

Tambahkan kode `javascript` berikut dibawah kode `css` diatas

```
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/>
```

### 2.2.3 Menambahkan map \<div>

Step berikutnya adalah menambahkan element `<div>` di dalam `<body>.` `<div>` ini kita gunakan sebagai block dari web yang akan ditampilkan. Setiap `div` harus memiliki `id` yang menyertai. Dalam tutorial ini kita gunakan `id` dengan nama `map`. Sehingga kode `div` menjadi

```
<div id="map"> </div>
```

agar map yang ditampilkan bisa memenuhi layar maka perlu menambahkan kode `css` berikut di antara `<head>`

```
body {
    padding: 0;
    margin: 0;
}
html, body, #map {
    height: 100%;
    width: 100%;
}
```

### 2.2.4 Menambahkan object map

Sekarang library leaflet sudah siap untuk digunakan. Untuk menampilkan map pada web kita perlu mengetahui koordinat dari suatu lokasi. Kita bisa menggunakan bantuan dari Google Map. Buka lokasi yang akan dituju menggunakan Google Map kemudian copy url dari lokasi tersebut. Contoh berikut ini merupakan url ketika membuka map UMS

```
https://www.google.com/maps/@-7.5579727,110.7696624,17z
```

Berdasar url tersebut maka koordinat kampus 1 UMS adalah \[-7.5579727, 110.7696624]

Langkah selanjutnya adalah memanggil fungsi leaflet dengan menggunakan koordinat diatas. Tambahkan kode berikut dibawah `<div id="map"></d`iv>

```
let map = L.map("map", { center: [-7.5580281, 110.7694159], zoom: 17 });
```

Save kemudian buka `index.htm`l melalui browser. Yang tampil hanya box dengan warna abu-abu. Untuk itu kita perlu menambahkan tile layer sesuai denga provider map yang akan digunakan. Pada tutorial ini kita akan menggunakan map dari OpenStreetMap. OpenStreetMap merupakan salah satu database gratis yang menyediakan tampilan map untuk seluruh dunia

Tambahkan kode berikut dibawah `let map` untuk menggunakan map dari OpenStreetMap

```
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="http://' +
          'www.openstreetmap.org/copyright">OpenStreetMap</a>',
      }).addTo(map);
```

Sehingga file `index.html` kita menjadi seperti berikut :&#x20;

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Basic Map</title>
    <link
      rel="stylesheet"
      href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
      integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
      crossorigin=""
    />
    <script
      src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
      integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
      crossorigin=""
    ></script>
    <style>
      body {
        padding: 0;
        margin: 0;
      }
      html,
      body,
      #map {
        height: 100%;
        width: 100%;
      }
    </style>
  </head>
  <body>
    <div id="map"></div>
    <script>
      let map = L.map("map", { center: [-7.5580281, 110.7694159], zoom: 17 });
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
          '&copy; <a href="http://' +
          'www.openstreetmap.org/copyright">OpenStreetMap</a>',
      }).addTo(map);
    </script>
  </body>
</html>

```

Jika kita buka file tersebut melalui browser maka akan menampilkan map dari kampus 1 UMS

![Web Map Pertama](<../.gitbook/assets/image (4).png>)

## 2.3 Menambahkan Vector Layer

Vector layer merupakan kumpulan suatu point, garis atau poligon yang dapat kita gunakan untuk menambahkan unsur interaktif ke dalam map

### 2.3.1 Menambahkan Marker

Untuk menambahkan marker kita menggunakan fungsi `L.marker`. Fungsi ini akan membuat objek marker pada peta. Ketika membuat marker kita perlu mengetahui letak koordinat dari marker tersebut. Seperti pada saat langkah menentukan peta kita dapat menggunakan bantuan google map untuk mencari lokasi koordinat marker. Misal kita ingin mencari koordinat titik di fakultas FKIP&#x20;

![Lokasi FKIP](<../.gitbook/assets/image (2) (1) (1).png>)

lihat pada url tersebut maka kita akan mendapatkan lokasi koordinat \[-7.5584646,110.7679351]

Bagaimana jika kita ingin mencari lokasi yang belum ada di Google Map. Caranya cukup mudah, buka lokasi tersebut melalui Google Map kemudian tekan dan tahan kursor pada titik yang akan dicari koordinatnya. Maka akan muncul popup yang berisi lokasi koordinatnya.

![Mencari lokasi koordinat](<../.gitbook/assets/image (2) (1).png>)

Setelah mengetahui titik koordinat maka langkah selanjutnya kita bisa membuat kode seperti berikut. Letakkan kode berikut setelah kode pembuatan `tilelayer` dan sebelum `</body>`

```
let marker_fkip = L.marker([-7.5584646,110.7679351]).addTo(map);
```

### 2.3.2 Menambahkan Popup

Agar lebih interaktif, biasanya marker kalau kita klik akan muncul pop up yang menjelaskan lokasi titik tersebut. Tambahkan kode berikut untuk membuat popup pada marker

```
  marker_fkip.bindPopup("<b>Kampus FKIP</b><br>Universitas Muhammadiyah Surakarta").openPopup();
```

Buka file index.html melalui browser maka bentuk map yang kita buat dapat dilihat pada tampilan berikut. Untuk melihat kode lengkapnya klik pada button HTML

{% embed url="https://codepen.io/cyanohumanos/pen/jOGqEmQ" %}
