<script lang="ts">
  import * as maptilersdk from '@maptiler/sdk';
  import { Alert, Button } from 'flowbite-svelte';

  maptilersdk.config.apiKey = 'aQhm9yzeHN2EnPoVqMPB';
  maptilersdk.config.primaryLanguage = maptilersdk.Language.JAPANESE;

  let currentMaker: maptilersdk.Marker | null = null;
  let position: [number, number] | null = null;
  let clicked = false;

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

    map.on('click', (event) => {
      const coordinates: [number, number] = [event.lngLat.lng, event.lngLat.lat];

      if (currentMaker) {
        currentMaker.remove();
      }

      currentMaker = new maptilersdk.Marker()
        .setLngLat(coordinates)
        .addTo(map);

      const pos = currentMaker.getLngLat();
      position = [parseFloat(pos.lng.toFixed(2)), parseFloat(pos.lat.toFixed(2))]
    });
  };

  const clickedOn = () => {
    clicked = true
  }

  const clickedOff = () => {
    clicked = false
  }
</script>

<div use:initMap style="height: 100vh;" />

<div class="fixed bottom-16 left-1/2 transform -translate-x-1/2">
  <Button disabled={currentMaker === null} on:click={clickedOn} color="blue" class="py-2 px-6 rounded-full shadow-lg focus:outline-none">この場所に設定する</Button>
</div>

{#if clicked}
  <div class="fixed top-4 left-1/2 transform -translate-x-1/2">
    <Alert border dismissable on:close={clickedOff} color="green" class="w-[300px]">👍 設定しました ({position})</Alert>
  </div>
{/if}
