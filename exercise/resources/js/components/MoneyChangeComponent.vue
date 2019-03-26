<template>
  <div class="card mt-3">
    <div class="card-body">
      <div
        class="alert alert-warning text-center"
        role="alert"
      >
        <strong>Money Change</strong>
      </div>
      <div class="row">
        <!-- 1 ฿ coins -->
        <div class="col-6">
          <div class="input-group">
            <div class="input-group-prepend">
              <span class="input-group-text">1</span>
            </div>
            <input
              type="text"
              class="form-control"
              :value="one"
              disabled
            >
          </div>
        </div>
        <!-- 2 ฿ coins -->
        <div class="col-6">
          <div class="input-group">
            <div class="input-group-prepend">
              <span class="input-group-text">2</span>
            </div>
            <input
              type="text"
              class="form-control"
              :value="two"
              disabled
            >
          </div>
        </div>
        <!-- 5 ฿ coins -->
        <div class="col-6 mt-2">
          <div class="input-group">
            <div class="input-group-prepend">
              <span class="input-group-text">5</span>
            </div>
            <input
              type="text"
              class="form-control"
              :value="five"
              disabled
            >
          </div>
        </div>
        <!-- 10 ฿ coins -->
        <div class="col-6 mt-2">
          <div class="input-group">
            <div class="input-group-prepend">
              <span class="input-group-text">10</span>
            </div>
            <input
              type="text"
              class="form-control"
              :value="ten"
              disabled
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["coinsChange"],
  mounted() {},
  data() {
    return {
      ten: 0,
      five: 0,
      two: 0,
      one: 0
    };
  },
  methods: {
    CoinClassification(coins) {
      if (coins / 10 != 0) {
        this.ten = parseInt(coins / 10);
        coins = parseInt(coins % 10);
      }
      if (coins / 5 != 0) {
        this.five = parseInt(coins / 5);
        coins = parseInt(coins % 5);
      }
      if (coins / 2 != 0) {
        this.two = parseInt(coins / 2);
        coins = parseInt(coins % 2);
      }
      this.one = coins;
      console.log(this.one);
      
      setTimeout(() => this.clearResult(), 7000);
    },
    clearResult() {
      this.$emit('clearCoinChange', 0);
      this.ten = 0;
      this.five = 0;
      this.two = 0;
      this.one = 0;
    }
  },
  watch: {
    coinsChange() {
      this.CoinClassification(this.coinsChange);
    }
  }
};
</script>
