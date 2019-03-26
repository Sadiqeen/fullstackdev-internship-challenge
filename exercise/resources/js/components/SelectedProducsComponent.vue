<template>
  <div class="card mt-3">
    <div class="card-body">
      <div
        class="alert alert-success text-center"
        role="alert"
      >
        <strong>Selected</strong>
      </div>
      <div
        v-for="product in productsSelected"
        :key="product.id"
      >
        <button class="btn btn-secondary btn-block mb-2">{{ product.productsName }} : {{ product.productsPrice }} Bath</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["productsSelected"],
  mounted() {},
  methods: {}
};
</script>
