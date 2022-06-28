<script>
import axios from 'axios';

export default {
  data: () => ({
    products : []
  }),
  created() {
    axios.get('http://yii2vue2/api/products')
      .then((response) => {
        //console.log(response.data)
        this.products = response.data
      })
  }
}
</script>

<template>
  <div class="about">
    <h1>Products</h1>
    <div id="products">
      <ul v-if="products && products.length">
        <li v-for="(product, index) of products" :key="index">
          {{ product.caption }} - {{ product.price }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
  }
}
</style>
