<template>
  <div class="container" v-if="!visualizzaForm">
    <div class="container">
      <div class="row py-2">
        <div class="col-8 text-left">
          <h1>Parametri Pair</h1>
        </div>
        <div class="col-4 text-right">
          <i class="fas fa-plus-circle" @click="prepareInsert()"></i>
        </div>
      </div>
    </div>
    <table class="table table-striped">
      <thead class="thead-dark">
        <tr>
          <th>First</th>
          <th>Second</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) of list" :key="index">
          <td>{{ row.first_cv}}</td>
          <td>{{ row.second_cv}}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <div class="container bg bg-light border rounded py-3" v-if="visualizzaForm">
    <h2 class="bg-white">Crea</h2>
    <div class="container">
      <form @submit.prevent="saveEntity">
        <div class="form-group row justify-content-md-center">
          <label for="first" class="col-2">First:</label>
          <div class="col-2">
            <input
              type="text"
              class="form-control"
              v-model="parametroPair.first_cv"
              maxlength="3"
              style="text-transform:uppercase"
            />
          </div>
        </div>
        <div class="form-group row justify-content-md-center">
          <label for="second" class="col-2">Second:</label>
          <div class="col-2">
            <input
              type="text"
              class="form-control"
              v-model="parametroPair.second_cv"
              maxlength="3"
              style="text-transform:uppercase"
            />
          </div>
        </div>
        <div class="form-group row justify-content-md-center">
          <div class="col-2"></div>
          <div class="col-2">
            <button type="submit" class="btn btn-block btn-primary">Crea</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      list: [],
      parametroPair: {},
      visualizzaForm: false,
    };
  },
  created() {
    axios
      .get("https://gcrypto.herokuapp.com/parametro-pair-cvs")
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
  methods: {
    saveEntity() {
      console.log("entità", this.entity);
      return axios
        .post("http://localhost:5000/parametro-pair-cvs", this.parametroPair, {
          headers: {
            Accept: "application/json",
            "Content-type": "application/json",
          },
        })
        .then(function (response) {
          return response.data;
        })
        .catch(function (error) {
          console.log("errore ", error);
          return "An error occured.." + error;
        });
    },
    prepareInsert() {
      this.visualizzaForm = true;
    },
  },
};
</script>