<template>
  <div class="home">
    <Navbar />
    <HeroCarousel />
    <WomenBanner />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import HeroCarousel from '../components/HeroCarousel.vue'
import WomenBanner from '../components/WomenBanner.vue'

export default {
  name: 'Home',
  components: {
    Navbar,
    HeroCarousel,
    WomenBanner,
  }
}
</script>
