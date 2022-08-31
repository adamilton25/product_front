<template>
    <h1>Editar Produto</h1>
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