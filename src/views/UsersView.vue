<script>
import axios from 'axios';

export default {
  data: () => ({
    users : []
  }),
  created() {
    axios.get('http://yii2vue2/api/users')
      .then((response) => {
        //console.log(response.data)
        this.users = response.data
      })
  }
}
</script>

<template>
  <div class="about">
    <h1>Users</h1>
    <div id="users">
      <ul v-if="users && users.length">
        <li v-for="(user, index) of users" :key="index">
          {{ user.name }} ({{ user.email }}, {{ user.phone }}, {{ user.password }})<br>
          Заказов: {{ user.orders.length }}
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
