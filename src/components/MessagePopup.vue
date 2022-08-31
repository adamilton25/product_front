<template>

    <div class="home">
    <h3>Deseja Realmente excluir o Produto?</h3>
    <div class="btns">
        <button>Não</button>
    </div>
    <button @click="deleteObject"></button>
    </div>
</template>

<style scoped>
    .btns button {
        margin: 10px 5px;
        padding: 10px 25px;
        background: blue;
        color: white;
        font-weight: 600;
        font-size: 15px;
        border: none;
    }
    .home{
      width: 50%;
      padding:  10px 150px;
      background: #fff;
      z-index: 3;
      top: 5%;
      right: 0;
      left: 0;
      margin: auto;
      padding: 50px;
      box-shadow:
  2.8px 2.8px 2.2px rgba(0, 0, 0, 0.02),
  6.7px 6.7px 5.3px rgba(0, 0, 0, 0.028),
  12.5px 12.5px 10px rgba(0, 0, 0, 0.035),
  22.3px 22.3px 17.9px rgba(0, 0, 0, 0.042),
  41.8px 41.8px 33.4px rgba(0, 0, 0, 0.05),
  100px 100px 80px rgba(0, 0, 0, 0.07)
;
    animation: fadeup 0.5s;
    position: absolute;
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
        name: 'MessagePopup',
        props: {
            product_id: Number
        },
        methods: {
            deleteObject(){
                axios
                .delete(`http://127.0.0.1:3000/v1/products/${this.product_id}`)
                .then(() => {
                this.$router.go();
            })
            }
        }
    }
</script>