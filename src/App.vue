<template>
  <div id="app">
    <div class="head-wrapper">
      <HeaderAni />
    </div>
    <div class="carousel-wrapper">
      <LogoCarousel v-if="!isMobile" />
      <MobileCarousel v-else-if="isMobile" />
    </div>
    <div class="body-cont">
      <div class="projects-wrapper">
        <Projects />
      </div>
      <div class="project-images-wrapper">
        <ProjectImages />
      </div>
      <div class="footer-container">
        <Footer />
      </div>
    </div>
  </div>
</template>

<script>
import HeaderAni from './components/TopAni.vue'
import LogoCarousel from './components/LogoCarousel.vue'
import Projects from './components/Projects.vue'
import ProjectImages from './components/ProjectImages.vue'
import Footer from './components/Footer.vue'
import MobileCarousel from './components/MobileCarousel.vue'
import { isMobile } from 'mobile-device-detect'
export default {
  name: 'App',
  components: {
    HeaderAni,
    LogoCarousel,
    Projects,
    ProjectImages,
    Footer,
    MobileCarousel
  },
  setup() {
    return { isMobile }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@300&display=swap');
body {
  margin: 0;
  overflow-x: hidden;
  font-family: 'Raleway', sans-serif;
}

html {
  overflow-x: hidden;
}

.projects-wrapper {
  margin-top: 225px;
  width: 100%;
  color: rgb(221, 221, 221);
  background-color: rgb(48, 48, 48);
}

.projects-wrapper {
  text-align: center;
}

.body-cont {
  position: absolute;
  top: 76%;
  width: 100%;
}

button {
  display: none;
}
</style>
