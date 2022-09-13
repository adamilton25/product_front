<template>
  <div class="about">
    <h4>{{items.length}} Items</h4>
    <table class="table">
  <thead class="table-dark">
    <tr>
      <th scope="col">Id</th>
      <th scope="col">Nome</th>
      <th scope="col">Descrição</th>
      <th scope="col">Valor</th>
      <th scope="col">Quantidade</th>
      <th scope="col">Actions</th>
    </tr>
  </thead>
  <tbody  v-for="(item) in items" :key="item.id" style="background:#111;color:#fff">
    <tr>
      <th scope="row">{{item.id}}</th>
      <td>{{item.name}}</td>
      <td>{{item.description.substring(0,50)}}</td>
      <td>{{item.value == null ? 'Valor não definido' : `R$${item.value}`}}</td>
      <td>{{parseInt(item.quantity) <= 0 ? 'Out of Stock' : parseInt(item.quantity) }}</td>
      <button @click="deleteProduct(item.id)" 
      style="border:none;background:red;color:aliceblue;padding:5px;">Excluir</button>
      <button  @click="editProduct(item.id)" 
      style="border:none;background:green;color:aliceblue;padding:5px;margin-left: 5px;
      ">Editar</button>
    </tr>
  </tbody>
  </table>
  <FormEdit v-if="edit" :product_id="product_id"/>
  <button  
      v-if="edit"
      @click="edit = !edit"
      style="border:none;
      background:red;
      color:aliceblue;
      padding:5px;
      margin-left: 5px;
      position: absolute;
      right: 45px;
      top: 90%;
      ">Close</button>
      </div>
</template>
<style scoped>
  td {
    font-size: 10px;
    width: 50px;
  }
  th {
    font-size: 10px;
    width: 10px;
  }
  tr
  {
    font-size: 10px;
  }
</style>
<script>
  import axios from 'axios';
import FormEdit from '@/components/FormEdit.vue';

  export default {
    name: "AboutView",
    data() {
        return {
            items: [],
            delete: "",
            edit: false,
            product_id: ''
        };
    },
    methods: {
        showAllProducts() {
            axios
                .get("http://127.0.0.1:3000/v1/products")
                .then((response) => {
                this.items = response.data.products;
            });
        },
        deleteProduct(id) {
            axios
                .delete(`http://127.0.0.1:3000/v1/products/${id}`)
                .then(() => {
                this.$toast.error(`Produto deletado!`, {
                    position: "top"
                });
                axios
                    .get("http://127.0.0.1:3000/v1/products")
                    .then((response) => {
                    this.items = response.data.products;
                });
            });
        },
        editProduct(id){
          this.product_id = id
          this.edit = true;
        }
    },
    mounted(){
        this.showAllProducts();
    },
    components: { FormEdit }
}
</script>
