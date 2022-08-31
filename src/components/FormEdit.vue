<template>
    <h1>Editar Produto</h1>
    <div class="home">
    <form @submit="EditItem" method="post">
      <label>Nome Produto</label>
      <input placeholder="Ex: Eletrodo" type="text" v-model="name"/>
      <label>Descrição Produto</label>
      <textarea placeholder="Ex: Produto usado para ..." type="text" v-model="description"/>
      <label>Quantidade</label>
      <input  placeholder="Ex: 10" type="number" v-model="quantity"/>
      <label>Valor</label>
      <input  placeholder="Ex: 10" type="number" v-model="value"/>
      <button type="submit">Editar Produto</button>
    </form>
  </div>
</template>
<style scoped>
    .home{
      width: 50%;
      padding:  10px 150px;
      background: #fff;
      z-index: 3;
      position: absolute;
      top: 5%;
      padding: 50px;
      right: 10%;
      box-shadow:
  2.8px 2.8px 2.2px rgba(0, 0, 0, 0.02),
  6.7px 6.7px 5.3px rgba(0, 0, 0, 0.028),
  12.5px 12.5px 10px rgba(0, 0, 0, 0.035),
  22.3px 22.3px 17.9px rgba(0, 0, 0, 0.042),
  41.8px 41.8px 33.4px rgba(0, 0, 0, 0.05),
  100px 100px 80px rgba(0, 0, 0, 0.07)
;
    animation: fadeup 1s;
    }
    
    .home form input, textarea {
      width: 100%;
      padding: 10px;
      outline: none;
      margin: 10px 0px;
    }
    .home form button{
      width: 100%;
      padding: 8px;
      border: none;
      background: #111111;
      color: white;
      font-weight: 600;
    }

    @keyframes fadeup{
        0%{
            transform: translateY(50px);
        }
    }
</style>

<script>
import axios from 'axios';

    export default {
        name: 'FormEdit',
        props: {
            product_id: Number
        },
        data(){
            return {
            item: {},
            name: '',
            description: '',
            quantity:'',
            value: '',
            }
        },
        methods: {
            getItem(){
              axios
              .get(`http://127.0.0.1:3000/v1/products/${this.product_id}`)  
              .then((response)=>{
                this.name = response.data.product.name
                this.description = response.data.product.description
                this.value = response.data.product.value
                this.quantity = response.data.product.quantity
              })
        },
        EditItem(e){
            e.preventDefault();
              axios
              .put(`http://127.0.0.1:3000/v1/products/${this.product_id}`,{
                    product: {
                    name: this.name,
                    description: this.description,
                    quantity: this.quantity,
                    value: this.value
                }
              })  
              .then(()=>{
                this.$toast.success(`Produto editado!`, {
                    position: "top"
                });
              })
        },
    },
    mounted() {
            this.getItem();
        }
    }
</script>