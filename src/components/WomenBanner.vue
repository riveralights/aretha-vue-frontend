<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length > 0">
          <carousel class="product-slider" :dots="true" :nav="false" :autoplay="true" :margin="25">
            <div class="product-item" v-for="product in products" :key="product.id">
              <div class="pi-pic">
                <img v-bind:src="product.galleries[0].photo" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view">
                    <router-link to="/product">+ Quick View</router-link>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{ product.type }}</div>
                <a href="#">
                  <h5>{{ product.name }}</h5>
                </a>
                <div class="product-price">
                 {{ product.price }}
                  <span>$85.00</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>
        <div class="col-lg-12" v-else>
          <p>Data Not Found</p>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>

<script>
import carousel from "vue-owl-carousel";
import axios from 'axios';

export default {
    name: 'WomenBanner',
    components: {
        carousel,
    },
    data() {
      return {
        products: []
      }
    },
    mounted() {
      axios
        .get('http://127.0.0.1:8000/api/product')
        .then(result => (this.products = result.data.data.data))
        .catch(error => console.log(error));
    }
}
</script>

<style>
.owl-theme .owl-dots .owl-dot span {
    width: 10px;
    height: 10px;
    margin: 5px 7px;
    background: #D6D6D6;
    display: block;
    -webkit-backface-visibility: visible;
    transition: opacity 200ms ease;
    border-radius: 30px;
    display: none;
}
</style>