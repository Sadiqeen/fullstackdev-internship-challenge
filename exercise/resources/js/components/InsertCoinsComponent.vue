<template>
  <div class="card mt-3">
    <div class="card-body">
      <div class="alert alert-success text-center" role="alert">
        <strong>Insert Coin</strong>
      </div>
      <div class="row">
        <div class="col-sm-3">
          <button class="btn btn-secondary btn-block" @click="addCoins(1)">1</button>
        </div>
        <div class="col-sm-3">
          <button class="btn btn-secondary btn-block" @click="addCoins(2)">2</button>
        </div>
        <div class="col-sm-3">
          <button class="btn btn-secondary btn-block" @click="addCoins(5)">5</button>
        </div>
        <div class="col-sm-3">
          <button class="btn btn-secondary btn-block" @click="addCoins(10)">10</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  mounted() {},
  methods: {
    addCoins(coins) {
      this.$emit('addCoins', coins);
    }
  }
};
</script>
