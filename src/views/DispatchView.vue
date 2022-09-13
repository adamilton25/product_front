<template>
     <div class="home">
      <div v-on:keyup.enter="GetProduct">
      <label>Id Produto</label>
      <input type="number" v-model="id" @click='message = !message' placeholder="Id do Produto"/>
      <b v-if="message">Aperte enter para pesquisar o produto</b><br/>
      <label>Produto</label>
      <input type="text" v-model="name" readonly/>
      <label>Descrição Produto</label>
      <textarea type="text" v-model="description" readonly/>
      <label>Quantidade</label>
      <input  placeholder="Ex: 10" type="number" v-model="quantity" readonly/>
      <label>Valor</label>
      <input type="number" v-model="value" readonly/><br/>
      <label>Quantidade de retirada</label>
      <input placeholder="Ex: 10" type="number" v-model="less_quantity"/>
      <button @click="removeQuantity">Retirar</button>
      </div>
</div>
</template>
<style scoped>
.home{
  width: 100%;
  padding:  10px 250px;
}

.home input, textarea {
  width: 100%;
  padding: 10px;
  outline: none;
  border-radius: 12px;
  outline: none;
  border: 1px solid #ccc;
}
.home button{
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
        name: 'DispatchView',
        data(){
            return {
                description: '',
                name: '',
                id:'',
                quantity: '',
                value: '',
                less_quantity: '',
                message: false
            }
        },
        methods: {
            GetProduct(){
              axios
              .get(`http://127.0.0.1:3000/v1/products/${this.id}`)  
              .catch(()=>{
                console.log('error');
                this.$toast.error(`Product não encontrado`,{
                position: 'top'
        });
              })
              .then((response)=>{
                console.log(response.data);
                this.name = response.data.product.name
                this.description = response.data.product.description
                this.value = response.data.product.value
                this.quantity = response.data.product.quantity
                this.message = false;
              })
            },
            removeQuantity(){
              axios
              .put(`http://127.0.0.1:3000/v1/products/${this.id}`,{
                    product: {
                    quantity: parseInt(this.quantity) - parseInt(this.less_quantity)
                }
              })  
              .then(()=>{
                this.$toast.success(`Produto retirado!`, {
                    position: "top"
                });
                this.GetProduct();
              })
            }
        }
    }
</script>