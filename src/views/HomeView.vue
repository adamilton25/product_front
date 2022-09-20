<template>
  <div class="home">
    <form @submit="CreateProduct" method="post">
      <label>Nome Produto</label>
      <input placeholder="Ex: Eletrodo" type="text" v-model="name" label=""/>
      <label>Descrição Produto</label>
      <textarea placeholder="Ex: Produto usado para ..." type="text" v-model="description"/>
      <label>Quantidade</label>
      <input  placeholder="Ex: 10" type="number" v-model="quantity" />
      <label>Valor</label>
      <input  placeholder="Ex: 10" type="number" v-model="value" />
      <button type="submit">Criar Produto</button>
    </form>
  </div>
</template>
<style scoped>
.home{
  width: 100%;
  padding:  10px 250px;
}
.home form input, textarea {
  width: 100%;
  padding: 10px;
  outline: none;
  border-radius: 12px;
  border: 1px solid #ccc;
}
.home form button{
  margin: 50px 0px;
  width: 100%;
  padding: 8px;
  background: #111111;
  color: white;
  font-weight: 600;
  border-radius: 12px;
  outline: none;
  border: 1px solid #ccc;
}
</style>
<script>
import axios from 'axios';

export default {
  name: 'HomeView',
  data(){
    return {
      name: '',
      description: '',
      quantity:'',
      value: ''
    }
  },
  methods: {
    CreateProduct(e){
      e.preventDefault();
      axios
      .post(`http://127.0.0.1:3000/v1/products`,{
          product:{
            name: this.name,
            description: this.description,
            quantity: this.quantity,
            value: this.value
          }
      })
      .then(() => {
        this.$toast.success(`Produto criado`,{
          position: 'top'
        });
      })
    }
  }
}
</script>
