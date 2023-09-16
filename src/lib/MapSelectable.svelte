<script lang="ts">
  import * as maptilersdk from '@maptiler/sdk';

  maptilersdk.config.apiKey = 'aQhm9yzeHN2EnPoVqMPB';
  maptilersdk.config.primaryLanguage = maptilersdk.Language.JAPANESE;

  let currentMaker: maptilersdk.Marker | null = null;

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

      if (currentMaker) {
        currentMaker.remove();
      }

      currentMaker = new maptilersdk.Marker()
        .setLngLat(coordinates)
        .addTo(map);
    });
  };
</script>

<div use:initMap style="height: 100vh;" />
