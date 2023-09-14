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
  };
</script>

<div use:initMap style="height: 100vh;" />
