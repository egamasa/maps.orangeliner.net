<script>
  import { onMount } from 'svelte';
  import L from 'leaflet';
  import 'leaflet/dist/leaflet.css';

  let map;

  onMount(() => {
    map = L.map('map').setView([35.658068, 139.751599], 16);

    const gsiPaleTileLayer = L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png', {
      attribution: '<a href="https://maps.gsi.go.jp/development/ichiran.html" target="_blank">地理院タイル</a>'
    }).addTo(map);

    const gsiPhotoTileLayer = L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/seamlessphoto/{z}/{x}/{y}.jpg', {
      attribution: '<a href="https://maps.gsi.go.jp/development/ichiran.html" target="_blank">地理院タイル</a>'
    });

    const gsiPhoto1970TileLayer = L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/gazo1/{z}/{x}/{y}.jpg', {
      attribution: '<a href="https://maps.gsi.go.jp/development/ichiran.html" target="_blank">地理院タイル</a>'
    });

    const gsiPhoto1960TileLayer = L.tileLayer('https://cyberjapandata.gsi.go.jp/xyz/ort_old10/{z}/{x}/{y}.png', {
      attribution: '<a href="https://maps.gsi.go.jp/development/ichiran.html" target="_blank">地理院タイル</a>'
    });

    L.control
      .layers({
        地理院タイル: gsiPaleTileLayer,
        地理院写真: gsiPhotoTileLayer,
        '地理院写真（1970年代）': gsiPhoto1970TileLayer,
        '地理院写真（1960年代）': gsiPhoto1960TileLayer
      })
      .addTo(map);

    L.marker([35.658068, 139.751599]).addTo(map).bindPopup('A pretty CSS3 popup.<br> Easily customizable.').openPopup();
  });
</script>

<div id="map"></div>
