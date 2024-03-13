<script setup>
import WR360 from '@webrotate360/imagerotator';
import { onMounted, onUnmounted } from 'vue';

let viewerApi;

onMounted(() => {
  const viewer = WR360.ImageRotator.Create('webrotate360');
  viewer.licenseCode = 'your-license-code';
  viewer.settings.configFileURL = '/example/example.xml';
  viewer.settings.graphicsPath = '/graphics';
  viewer.settings.alt = 'Your alt image description';
  viewer.settings.responsiveBaseWidth = 800;
  viewer.settings.responsiveMinHeight = 300;
  viewer.settings.apiReadyCallback = (api, isFullScreen) => {
    viewerApi = api;
    viewerApi.images.onDrag((event) => {
      console.log(`${event.action}; current image index = ${viewerApi.images.getCurrentImageIndex()}`);
    });
  };

  viewer.runImageRotator();
});

onUnmounted(() => {
  if (viewerApi) {
    console.log('Destroying Webrotate...');
    viewerApi.delete();
  }
});
</script>

<template>
  <div class="alignCenter">
    <div class="viewerContainer">
      <div id="webrotate360"></div>
    </div>
  </div>
</template>
