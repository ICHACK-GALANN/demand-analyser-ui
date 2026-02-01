<script lang="ts" setup>
import Globe from 'globe.gl'

const globeRef = useTemplateRef<HTMLDivElement>('globeContainer')

onMounted(() => {
  if (!globeRef.value) return;

  const N = 60;
  const gData = [...Array(N).keys()].map(() => ({
    lat: (Math.random() - 0.5) * 160,
    lng: (Math.random() - 0.5) * 360,
    weight: Math.random()
  }));
  
  const globe = new Globe(globeRef.value!)
    .globeImageUrl('https://cdn.jsdelivr.net/npm/three-globe/example/img/earth-blue-marble.jpg')
    .heatmapsData([gData])
    .heatmapPointLat('lat')
    .heatmapPointLng('lng')
    .heatmapPointWeight('weight')
    .heatmapBandwidth(0.4)
    .heatmapColorSaturation(2.8)
    .onHeatmapClick((_data: object, _mEvent, { lat, lng }) => {
      const data = _data as { lat: number; lng: number; weight: number }[];
      const datapoint = data.find(d => Math.abs(d.lat - lat) < 1 && Math.abs(d.lng - lng) < 1);

      if (!datapoint) {
        console.warn('No datapoint found for clicked location');
        return;
      }
      navigateTo(`/details/id`);
    });

  globe.renderer().setPixelRatio(1)
})
</script>

<template>
  <div ref="globeContainer" class="w-full max-w-2lg overflow-hidden"></div>
</template>

<style>

</style>