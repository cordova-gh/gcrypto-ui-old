<template>
  <div class="about" v-if="!visualizzaForm">
    <h1>Parametri Pair</h1>
     <input type="button" class="btn btn-primary" value="Inserisci" @click="prepareInsert">
    <table class="table">
      <thead>
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
  <div class="container" v-if="visualizzaForm"> 
    <h2>Crea</h2>
    <form @submit.prevent="saveEntity">
   
      <div class="form-group">
        <label for="first">First:</label>
        <input type="text" class="form-control" v-model="parametroPair.first_cv" />
      </div>
      <div class="form-group">
        <label for="second">Second:</label>
        <input type="text" class="form-control" v-model="parametroPair.second_cv" />
      </div>
      <button type="submit" class="btn btn-primary">Crea</button>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      list: [],
      parametroPair: {},
      visualizzaForm: false
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
    prepareInsert(){
      this.visualizzaForm= true;
    }
  },
};
</script>