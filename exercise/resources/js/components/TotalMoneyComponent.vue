<template>
  <div class="card mt-3">
    <div class="card-body">
      <p class="h2">
        <i class="fas fa-coins"></i> : {{totalMoney}} Bath
      </p>
      <button
        class="btn btn-warning btn-block mt-3"
        @click="moneyChange(totalMoney)"
      >Money change</button>
      <p class="h3">
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["totalMoney"],
  mounted() {},
  methods: {
    moneyChange(totalMoney) {
      this.$parent.passCoinsChange(totalMoney);
    }
  }
};
</script>
