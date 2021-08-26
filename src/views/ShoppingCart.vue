<template>
  <div class="shopping">
    <Navbar />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <a href="./home.html"><i class="fa fa-home"></i> Home</a>
              <span>Shopping Cart</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8">
            <div class="row">
              <div class="col-lg-12">
                <div class="cart-table">
                  <table>
                    <thead>
                      <tr>
                        <th>Image</th>
                        <th class="p-name text-center">Product Name</th>
                        <th>Price</th>
                        <th>Action</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="cart in cartUser" :key="cart.id">
                        <td class="cart-pic first-row">
                          <img :src="cart.photo" />
                        </td>
                        <td class="cart-title first-row text-center">
                          <h5>{{ cart.name }}</h5>
                        </td>
                        <td class="p-price first-row">${{ cart.price }}.00</td>
                        <td class="delete-item" @click="removeCartItem(cartUser.index)">
                          <a href="#"><i class="material-icons"> X </i></a>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <div class="col-lg-8">
                <h4 class="mb-4">Informasi Pembeli:</h4>
                <div class="user-checkout">
                  <form>
                    <div class="form-group">
                      <label for="namaLengkap">Nama lengkap</label>
                      <input
                        type="text"
                        class="form-control"
                        id="namaLengkap"
                        aria-describedby="namaHelp"
                        placeholder="Masukan Nama"
                        v-model="customerInfo.name"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">Email Address</label>
                      <input
                        type="email"
                        class="form-control"
                        id="emailAddress"
                        aria-describedby="emailHelp"
                        placeholder="Masukan Email"
                        v-model="customerInfo.email"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">No. HP</label>
                      <input
                        type="text"
                        class="form-control"
                        id="noHP"
                        aria-describedby="noHPHelp"
                        placeholder="Masukan No. HP"
                        v-model="customerInfo.number"
                      />
                    </div>
                    <div class="form-group">
                      <label for="alamatLengkap">Alamat Lengkap</label>
                      <textarea
                        class="form-control"
                        id="alamatLengkap"
                        rows="3"
                        v-model="customerInfo.address"
                      ></textarea>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="row">
              <div class="col-lg-12">
                <div class="proceed-checkout">
                  <ul>
                    <li class="subtotal">
                      ID Transaction <span>#SH12000</span>
                    </li>
                    <li class="subtotal mt-3">Subtotal <span>${{ subPrice }}</span></li>
                    <li class="subtotal mt-3">Pajak <span>10% (${{ withTax }})</span></li>
                    <li class="subtotal mt-3">
                      Total Biaya <span>${{ totalPrice }}</span>
                    </li>
                    <li class="subtotal mt-3">
                      Bank Transfer <span>Mandiri</span>
                    </li>
                    <li class="subtotal mt-3">
                      No. Rekening <span>2208 1996 1403</span>
                    </li>
                    <li class="subtotal mt-3">
                      Nama Penerima <span>Shayna</span>
                    </li>
                  </ul>
                  <!-- <router-link to="/success" class="proceed-btn">I ALREADY PAID</router-link> -->
                  <a @click="checkout()" href="#" class="proceed-btn">I ALREADY PAID</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section End -->
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from 'axios';

export default {
  name: "ShoppingCart",
  components: {
    Navbar,
  },
   data() {
    return {
      cartUser: [],
      customerInfo: {
        name: "",
        email: "",
        number: "",
        address: "",
      }
    };
  },
  methods: {
    removeCartItem(index) {
      // hapus index item nya
      this.cartUser.splice(index, 1);
      // parsing data terbaru 
      const parsed = JSON.stringify(this.cartUser);
      // simpan hasil parsingan terbaru ke localstorage
      localStorage.setItem('cartUser', parsed);
    },

    checkout() {
      let productIds = this.cartUser.map(product => product.id);

      let checkoutData = {
        'name': this.customerInfo.name,
        'email': this.customerInfo.email,
        'address': this.customerInfo.address,
        'number': this.customerInfo.number,
        'transaction_total': this.totalPrice,
        'transaction_status': 'PENDING',
        'transaction_detail': productIds,
      };

      axios
        .post('http://127.0.0.1:8000/api/checkout', checkoutData)
        .then(() => this.$router.push('success'))
        .catch(error => console.log(error));
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
    subPrice() {
      return this.cartUser.reduce((accumulator, total) => {
        return accumulator + total.price;
      }, 0);
    },
    withTax() {
      return (this.subPrice * 10) / 100;
    },
    totalPrice() {
      return Math.round(this.subPrice + this.withTax);
    }
  }
};
</script>