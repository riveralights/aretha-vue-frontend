<template>
  <!-- Header Section Begin -->
  <header class="header-section">
    <div class="header-top">
      <div class="container">
        <div class="ht-left">
          <div class="mail-service">
            <i class="fa fa-envelope"></i> hello.aretha@gmail.com
          </div>
          <div class="phone-service">
            <i class="fa fa-phone"></i> +628 22081996
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="inner-header">
        <div class="row">
          <div class="col-lg-2 col-md-2">
            <div class="logo">
              <a href="./index.html">
                <img src="img/logo_website_shayna.png" alt="" />
              </a>
            </div>
          </div>
          <div class="col-lg-7 col-md-7"></div>
          <div class="col-lg-3 text-right col-md-3">
            <ul class="nav-right">
              <li class="cart-icon">
                Keranjang Belanja &nbsp;
                <a href="#">
                  <i class="icon_bag_alt"></i>
                  <span>{{ cartUser.length }}</span>
                </a>
                <div class="cart-hover">
                  <div class="select-items">
                    <table>
                      <tbody v-if="cartUser.length > 0">
                        <tr v-for="cart in cartUser" :key="cart.id">
                          <td class="si-pic">
                            <img :src="cart.photo" alt="" width="50"/>
                          </td>
                          <td class="si-text">
                            <div class="product-selected">
                              <p>${{ cart.price }} x 1</p>
                              <h6>{{ cart.name }}</h6>
                            </div>
                          </td>
                          <td @click="removeCartItem(cart.id)" class="si-close">
                            <i class="ti-close"></i>
                          </td>
                        </tr>
                      </tbody>
                      <tbody v-else>
                        <tr>
                          <td class="text-center">Keranjang Kosong</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                  <div class="select-total">
                    <span>total:</span>
                    <h5>${{ totalPrice }}.00</h5>
                  </div>
                  <div class="select-button">
                    <router-link to="/shopping-cart" class="primary-btn view-card">VIEW CARD</router-link>
                    <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
  <!-- Header End -->
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      cartUser: [],
    };
  },
  methods: {
    removeCartItem(idProduct) {
      let cartLocalStorage = JSON.parse(localStorage.getItem('cartUser'));
      let itemCartLocalStorage = cartLocalStorage.map(itemCartUserStorage => itemCartUserStorage.id);
      let index = itemCartLocalStorage.findIndex(id => id == idProduct);
      this.cartUser.splice(index, 1);

      const parsed = JSON.stringify(this.cartUser);
      localStorage.setItem('cartUser', parsed);
      window.location.reload();
    }
  },
  mounted() {
    // kalau localstorage ada isi nya yakni cartUser
    if(localStorage.getItem('cartUser')) {
      try {
        // ambil data cartUser, tapi parsing dulu
        this.cartUser = JSON.parse(localStorage.getItem('cartUser'));
      } catch(e) {
        // hapus isi cartUser
        localStorage.removeItem('cartUser');
      }
    }
  },
  computed: {
    totalPrice() {
      return this.cartUser.reduce((accumulator, total) => {
        return accumulator + total.price;
      }, 0);
    }
  }
};
</script>
