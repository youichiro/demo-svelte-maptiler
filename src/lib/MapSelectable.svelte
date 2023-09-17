<script lang="ts">
  import * as maptilersdk from '@maptiler/sdk';
  import { GeocodingControl } from "@maptiler/geocoding-control/maptilersdk";
  import { Button } from 'flowbite-svelte';

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
      // 日本のエリアに制限
      maxBounds: [
        [122.9332, 24.3963], // 南西端の座標
        [153.9867, 45.5515]  // 北東端の座標
      ]
    });

    const gc = new GeocodingControl();
    map.addControl(gc, 'top-left');

    map.on('click', (event) => {
      const coordinates: [number, number] = [event.lngLat.lng, event.lngLat.lat];

      if (currentMaker) {
        currentMaker.remove();
      }

      currentMaker = new maptilersdk.Marker()
        .setLngLat(coordinates)
        .addTo(map);

      const pos = currentMaker.getLngLat();
      console.log(pos)
    });
  };
</script>

<div use:initMap style="height: 100vh;" />

<div class="fixed bottom-16 left-1/2 transform -translate-x-1/2">
  <Button disabled={currentMaker === null} on:click={() => console.log("設定しました")} color="blue" class="py-2 px-6 rounded-full shadow-lg focus:outline-none">この場所に設定する</Button>
</div>
