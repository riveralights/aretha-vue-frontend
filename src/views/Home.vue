<template>
  <div class="home">
    <Navbar />
    <HeroCarousel />
    <WomenBanner />
    <InstagramGallery />
    <PartnerLogo />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import HeroCarousel from '../components/HeroCarousel.vue'
import WomenBanner from '../components/WomenBanner.vue'
import InstagramGallery from '../components/InstagramGallery.vue'
import PartnerLogo from '../components/PartnerLogo.vue'

export default {
  name: 'Home',
  components: {
    Navbar,
    HeroCarousel,
    WomenBanner,
    InstagramGallery,
    PartnerLogo,
  }
}
</script>
