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
                <div
                  class="product-thumbs"
                  v-if="productDetails.galleries.length > 0"
                >
                  <carousel
                    :dots="false"
                    :nav="false"
                    :margin="14"
                    class="product-thumbs-track ps-slider"
                  >
                    <div
                      v-for="productImage in productDetails.galleries"
                      :key="productImage.id"
                      class="pt"
                      :class="
                        productImage.photo == defaultImage ? 'active' : ''
                      "
                      @click="changeImage(productImage.photo)"
                    >
                      <img v-bind:src="productImage.photo" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3 class="my-4">{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p
                      v-html="productDetails.description"
                      class="text-justify"
                    ></p>
                    <h4 class="my-4">${{ productDetails.price }}.00</h4>
                  </div>
                  <div class="quantity">
                    <!-- <router-link to="/shopping-cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link
                    > -->
                    <router-link to="/shopping-cart"
                      ><a
                        href="#"
                        @click="
                          saveToCart(
                            productDetails.id,
                            productDetails.name,
                            productDetails.price,
                            productDetails.galleries[0].photo
                          )
                        "
                        class="primary-btn pd-cart"
                        >Add to Cart</a
                      ></router-link
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
import RelatedProduct from "../components/RelatedProduct.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";

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
      defaultImage: "",
      productDetails: [],
      cartUser: [],
    };
  },
  methods: {
    changeImage(imageUrl) {
      this.defaultImage = imageUrl;
    },
    setDataPicture(data) {
      // replace object productDetails dengan data dari API
      this.productDetails = data;
      // replance value default images dengan data dari API
      this.defaultImage = data.galleries[0].photo;
    },
    saveToCart(idProduct, nameProduct, priceProduct, photoProduct) {
      let productStored = {
        id: idProduct,
        name: nameProduct,
        price: priceProduct,
        photo: photoProduct,
      };

      this.cartUser.push(productStored);
      const parsed = JSON.stringify(this.cartUser);
      localStorage.setItem("cartUser", parsed);
    },
  },
  mounted() {
    if (localStorage.getItem("cartUser")) {
      try {
        this.cartUser = JSON.parse(localStorage.getItem("cartUser"));
      } catch (e) {
        localStorage.removeItem("cartUser");
      }
    }

    axios
      .get("http://127.0.0.1:8000/api/product", {
        params: {
          id: this.$route.params.id,
        },
      })
      .then((result) => this.setDataPicture(result.data.data))
      .catch((error) => console.log(error));
  },
};
</script>
