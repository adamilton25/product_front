<template>
  <div class="about">
    <table class="table">
  <thead class="table-dark">
    <tr>
      <th scope="col">Id</th>
      <th scope="col">Nome</th>
      <th scope="col">Descrição</th>
      <th scope="col">Valor</th>
      <th scope="col">Quantidade</th>
    </tr>
  </thead>
  <tbody>
    <tr :v-for="(item in items)" v-show="items != []">
      <th scope="row">{{item}}</th>
      <td>Mark</td>
      <td>Otto</td>
      <td>@mdo</td>
      <td>@mdo</td>
    </tr>
  </tbody>
  </table>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name:"AboutView",
    data(){
      return {
        items:[]
      }
    },
    methods: {
      showAllProducts(){
        axios 
        .get('http://127.0.0.1:3000/v1/products')
        .then((response) => {
          this.items = response.data['products'];
        }) 
      }
    },
    mounted(){
      this.showAllProducts();
    }
  }
</script>
