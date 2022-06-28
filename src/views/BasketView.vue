<script>
import axios from 'axios';

export default {
  props: ['id'],
  data: () => ({
    products : [],
  }),
  watch: {
    id: {
      handler(newId, oldId) {
        axios.get('http://yii2vue2/api/basket/'+newId)
          .then((response) => {
            this.products = response.data
          })
      },
      deep: true,
    }
  },
  mounted() {
    console.log(123)
    axios.get('http://yii2vue2/api/basket/'+this.id)
      .then((response) => {
        //console.log(response.data)
        this.products = response.data
      })
  },
}
</script>

<template>
  <h3>Детали корзины</h3>
  <div id="orders">
    <ul v-if="products && products.length">
      <li v-for="(product, index) of products" :key="index">
        {{ product.product.caption }} - {{ product.product.price }} руб.
      </li>
    </ul>
  </div>
</template>

