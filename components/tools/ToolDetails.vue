<template>
  <div class="card">
    <div class="product">
      <div class="product-image">
        <img :src="product.image" alt="Product Image">
      </div>
      <div class="product-details">
        <h3>{{ product.name }}</h3>
        <p>Tool ID: {{ product.id }}</p>
        <p>Warranty Date: {{ product.warranty }}</p>
        <p>Last Checked Time: {{ product.checktime }}</p>
        <p>Status: {{ product.status }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToolDetails',
  props: {
    // eslint-disable-next-line vue/require-default-prop
    product: Object // pass product data as props
  }
}
</script>

<style>
.product {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 20px;
  /* background-color: white; */
}

.product-image img {
  width: 200px;
  height: 200px;
  object-fit: contain;
  margin-right: 20px;
}

.product-details {
  flex: 1;
}

.product-details h3 {
  margin-top: 0;
}
</style>
