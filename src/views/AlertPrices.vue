<template>
  <div class="about">
    <h1>This is an alert prices page</h1>
    <table class="table">
      <thead>
        <th>ID</th>
        <th>Price</th>
        <th>Is support</th>
      </thead>
      <tbody>
        <tr v-for="(row, index) of list" :key="index">
          <td>{{ row.id_parametro_pair_cv}}</td>
          <td>{{ row.price}}</td>
          <td>{{ row.is_support}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      list: [],
    };
  },
  created() {
    axios
      .get("https://gcrypto.herokuapp.com/alert-prices")
      .then((response) => {
        this.list = response.data;
        console.log("sono solo un console ", response);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>