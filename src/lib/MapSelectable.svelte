<script lang="ts">
  import * as maptilersdk from '@maptiler/sdk';

  maptilersdk.config.apiKey = 'aQhm9yzeHN2EnPoVqMPB';
  maptilersdk.config.primaryLanguage = maptilersdk.Language.JAPANESE;

  const initMap = (container: HTMLElement) => {
    const map = new maptilersdk.Map({
      container: container,
      style: maptilersdk.MapStyle.STREETS,
      center: [139.7017, 35.6581], // 渋谷
      zoom: 12,
      fullscreenControl: true,
    });

    // タップイベントを追加
    map.on('click', (event) => {
      const coordinates: [number, number] = [event.lngLat.lng, event.lngLat.lat];

      // マーカーを作成して地図に追加
      new maptilersdk.Marker()
        .setLngLat(coordinates)
        .addTo(map);
    });
  };
</script>

<div use:initMap style="height: 100vh;" />
