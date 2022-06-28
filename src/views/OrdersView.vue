<script>
import axios from 'axios';
import BasketView from './BasketView.vue';

export default {
  components: {
    BasketView,
  },
  data: () => ({
    orders : [],
    compName: false,
    order_id: 0,
  }),
  created() {
    axios.get('http://yii2vue2/api/orders')
      .then((response) => {
        //console.log(response.data)
        this.orders = response.data
      })
  },
  methods: {
    details: function (id) {
      this.compName = 'BasketView';
      this.order_id = id;
    },
  },
}
</script>

<template>
  <div class="about">
    <h1>Orders</h1>
    <div id="orders">
      <ul v-if="orders && orders.length">
        <li v-for="(order, index) of orders" :key="index" @click="details(order.id)" class="order">
          {{ order.user.name }} - {{ order.summa }} руб.
        </li>
      </ul>
    </div>
    <hr/>
    <div v-if="compName">
      <component :is="compName" v-bind:id="order_id"></component>
    </div>
  </div>
</template>

<style>
.order {
  color: #1E90FF;
  cursor: pointer;
}
.order:hover {
  text-decoration: underline;
}
</style>
