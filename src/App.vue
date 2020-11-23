<template>
  <div id="app">
    <div class="head-wrapper">
      <HeaderAni />
    </div>
    <div class="carousel-wrapper">
      <LogoCarousel />
    </div>
  </div>
</template>

<script>
import HeaderAni from './components/TopAni.vue'
import LogoCarousel from './components/LogoCarousel.vue'
export default {
  name: 'App',
  components: {
    HeaderAni,
    LogoCarousel
  }
}
</script>

<style>
body {
  margin: 0;
  overflow-x: hidden;
}
</style>
