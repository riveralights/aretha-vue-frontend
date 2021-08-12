<template>
  <section class="hero-section">
    <carousel class="hero-items" :items="1" :nav="false" :loop="true" :autoplay="true" :dots="false">
      <div class="single-hero-items set-bg" style="background-image: url('/img/hero-1.jpg')">
        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <span>Woman</span>
              <h1>Black Friday</h1>
              <p>
                Temukan keuntungan dan penawaran menarik dalam event Black
                Friday Sale. Don't miss it!
              </p>
              <a href="#" class="primary-btn">Shop Now</a>
            </div>
          </div>
        </div>
      </div>
      <div class="single-hero-items set-bg" style="background-image: url('/img/hero-2.jpg')">
        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <span>Kids</span>
              <h1>Cool Kids</h1>
              <p>
                Diskon besar-besaran higga 80% khusus untuk pakaian anak-anak
                akhir pekan ini
              </p>
              <a href="#" class="primary-btn">Shop Now</a>
            </div>
          </div>
        </div>
      </div>
    </carousel>
  </section>
</template>

<script>
import carousel from "vue-owl-carousel";

export default {
  name: "HeroCarousel",
  components: {
    carousel,
  },
};
</script>