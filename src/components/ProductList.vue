<template>
  <div class="layout-row wrap justify-content-center">
    <section v-for="(product, index) in products"
             :key="index"
             :data-testid="'product-item-' + index"
             class="w-30 product-item">
      <div class="card ma-16">
        <img :src="product.image" class="product-image" :alt="product.name"/>
        <div class="card-text pa-4">
          <h5 class="ma-0 text-center">{{ product.name }}</h5>
          <p class="ma-0 mt-8 text-center">${{ product.price }}</p>
        </div>
        <div class="card-actions justify-content-center pa-4">
          <button
            class="x-small outlined"
            data-testid="btn-item-action"
            @click="toggleCart(product)"
          >
            {{ isInCart(product) ? "Remove From Cart" : "Add To Cart" }}
          </button>
        </div>
      </div>
    </section>
  </div>

</template>

<script>
export default {
  name: "ProductList",
  props: {
    products: Array
  },
  methods : {
    toggleCart(product) {
      this.$emit("toggleCart", product);
    },
    isInCart(product) {
      return product.cartQuantity > 0;
    },
    addToCart(product) {
      // Emit the addToCart event with the product as payload
      this.$emit("addToCart", product);
    },
    removeFromCart(product) {
      // Emit the removeFromCart event with the product as payload
      this.$emit("removeFromCart", product);
    }
  }
}
</script>

<style scoped lang="scss">

.product-image {
  margin: 32px 30%;
  width: 40%;
  min-height: 90px;
}

</style>
