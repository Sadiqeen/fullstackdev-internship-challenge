<template>
  <div class="row">
    <div class="col-md-9">
      <div class="row">
        <div
          v-for="product in products"
          :key="product.id"
          class="col-md-4 mt-3"
        >
          <div class="card">
            <img
              class="card-img-top"
              height="230"
              :src="product.image"
              alt
            >
            <div class="card-body">
              <h4 class="card-title">{{ product.name }}</h4>
              <p class="card-text">{{ product.price }}</p>
              <button
                v-if="product.in_stock == true"
                @click="selectProduct(product.id, product.price, product.name)"
                class="btn btn-success btn-block text-white"
              >เลือก</button>
              <button
                v-else
                class="btn btn-secondary btn-block text-white"
                disabled
              >สินค้าหมด</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-md-3">
      <total-money
        :totalMoney="totalMoney"
        @moneyChange="coinsChange($event)"
      ></total-money>
      <insert-coins
        :coins="totalMoney"
        @addCoins="totalMoney += $event"
      ></insert-coins>
      <money-change
        :coinsChange="coinsChange"
        @clearCoinChange="coinsChange = $event"
      ></money-change>
      <selected-products :productsSelected="productsSelected"></selected-products>
    </div>
  </div>
</template>

<script>
import totalMoney from "./TotalMoneyComponent";
import InsertCoins from "./InsertCoinsComponent";
import moneyChange from "./MoneyChangeComponent";
import SelectedProducts from "./SelectedProducsComponent";

export default {
  mounted() {
    this.getProducts();
  },
  data() {
    return {
      totalMoney: 0,
      coinsChange: 0,
      products: [],
      productsSelected: []
    };
  },
  methods: {
    getProducts() {
      axios
        .get("https://www.mocky.io/v2/5c77c5b330000051009d64c9")
        .then(response => {
          this.products = response.data.data;
        });
    },
    selectProduct(id, price, name) {
      if (price <= this.totalMoney) {
        this.totalMoney -= price;
        this.productsSelected.push({
          productsID: id,
          productsName: name,
          productsPrice: price
        });
      } else {
        this.$swal({
          type: 'error',
          title: 'Oops...',
          text: 'Please add more money!',
        });
      }
    },
    passCoinsChange(coinsChange) {
      this.totalMoney = 0;
      this.productsSelected = [];
      this.coinsChange = coinsChange;
    },
    clearProductsSelected() {
      this.productsSelected = [];
    }
  },
  components: {
    "total-money": totalMoney,
    "insert-coins": InsertCoins,
    "money-change": moneyChange,
    "selected-products": SelectedProducts
  },
  watch: {
    totalMoney(val, oldVal) {
      if (val == 0) {
        setTimeout(() => this.clearProductsSelected(), 7000);
      }
    }
  }
};
</script>
