<template>
  <div class="home">
    <Navbar />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="defaultImage" alt="" />
                </div>
                <div class="product-thumbs">
                  <carousel
                    :dots="false"
                    :nav="false"
                    :margin="14"
                    :loop="true"
                    class="product-thumbs-track ps-slider"
                  >
                    <div class="pt" :class="thumbnail[0] == defaultImage ? 'active' : ''" @click="changeImage(thumbnail[0])">
                      <img src="img/satin-1.png" alt="" />
                    </div>

                    <div class="pt" :class="thumbnail[1] == defaultImage ? 'active' : ''" @click="changeImage(thumbnail[1])">
                      <img src="img/satin-2.png" alt="" />
                    </div>

                    <div class="pt" :class="thumbnail[2] == defaultImage ? 'active' : ''"  @click="changeImage(thumbnail[2])">
                      <img src="img/satin-3.png" alt="" />
                    </div>

                    <div class="pt" :class="thumbnail[3] == defaultImage ? 'active' : ''" @click="changeImage(thumbnail[3])">
                      <img src="img/satin-4.png" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>Shirt</span>
                    <h3>Blue Satin Sleeve</h3>
                  </div>
                  <div class="pd-desc">
                    <p>
                      Sebuah kaos berwarna biru yang terbuat dari bahan satin
                      yang dilengkapi dengan pita membuat anda merasa cantik dan
                      percaya diri secara bersamaan.
                    </p>
                    <p>
                      Baju ini memiliki desain lengan yang panjang dan pattern
                      collar yang indah. Selendang dibuat dengan bahan yang sama
                      dan bentuk yang dikalkukasi sehingga menghasilkan desain
                      yang <em>assymetric</em>. Memiliki pola kancing dibagian
                      depan kaos sehingga pengguna dapat lebih mudah dan nyaman
                      dalam menggapai kancing. Baju ini memiliki warna biru
                      langit, sangat cocok untuk anda gunakan pada saat liburan
                      musim panas. Bagian luar dibuat dengan bahan 100% dari
                      polyester asli. Barang tersedia dalam berbagai ukuran dari
                      XS hingga XXL.
                    </p>
                    <p></p>
                    <h4>$72.50</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/shopping-cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProduct />

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";
import RelatedProduct from '../components/RelatedProduct.vue';
import carousel from "vue-owl-carousel";

export default {
  name: "Home",
  components: {
    Navbar,
    Footer,
    carousel,
    RelatedProduct,
  },
  data() {
      return {
          defaultImage: "img/satin-1.png",
          thumbnail: [
              'img/satin-1.png',
              'img/satin-2.png',
              'img/satin-3.png',
              'img/satin-4.png',
          ]
      }
  },
  methods: {
      changeImage(imageUrl) {
          this.defaultImage = imageUrl
      }
  }
};
</script>
