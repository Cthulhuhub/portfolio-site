<template>
  <div id="app">
    <div class="head-wrapper">
      <HeaderAni />
    </div>
    <div class="carousel-wrapper">
      <LogoCarousel />
    </div>
    <div class="projects-wrapper">
      <Projects />
    </div>
  </div>
</template>

<script>
import HeaderAni from './components/TopAni.vue'
import LogoCarousel from './components/LogoCarousel.vue'
import Projects from './components/Projects.vue'
export default {
  name: 'App',
  components: {
    HeaderAni,
    LogoCarousel,
    Projects
  }
}
</script>

<style>
body {
  margin: 0;
  overflow-x: hidden;
}

.projects-wrapper {
  margin-top: 12%;
  width: 100%;
  color: rgb(221, 221, 221);
  background-color: rgb(48, 48, 48);
}

.projects-wrapper {
  text-align: center;
}
</style>
