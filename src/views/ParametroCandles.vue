<template>
  <div class="about">
    <h1>This is a Candles page</h1>
      <table class="table">
        <thead>
          <tr>
            <th>ID</th>
            <th>First</th>
            <th>Second</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, index) of list" :key="index">
            <td>{{ row.id}}</td>
            <td>{{ row.first_cv}}</td>
            <td>{{ row.second_cv}}</td>
          </tr>
        </tbody>
      </table>
  </div>
  <form>
    <div class="form-group">
      Id:
      <select name="id_parametro_pair_cv">
        <option value="1">BTC/USDT</option>
      </select>      
      First:
      <input type="text" />
      Second:
      <input type="text" />

      <input type="submit" value="Invio" />
    </div>
  </form>
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
      .get("https://gcrypto.herokuapp.com/parametro-candle-cvs")

      .then((response) => {
        this.list = response.data;
        console.log(response);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>