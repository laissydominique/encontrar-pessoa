<script setup>
import { ref } from "vue";

const info = ref({
  id: null,
  dados: " ",
  erro: false,
});

async function teste() {
  const response = await fetch(
    `https://dummyapi.online/api/social-profiles/${info.value.id}`
  );
  const data = await response.json();
  console.log(data);

  info.value.dados = {
    nome: data.fullName,
    email: data.email,
    user: data.username,
    trabalho: data.work,
    cidade: data.location,
  };

  if (!data.userId) {
    info.value.erro = true;
  }else{
    info.value.erro = false;

  }
}
</script>

<template>
    <div class="container">    
      <h1>Busque pessoas pelo ID</h1>

    <div class="input">
  <input  v-model="info.id" type="text" placeholder="Digite ID aqui" /> </div>
  <div class="botao">
  <button @click="teste"> Consultar </button>
</div>
<div class="infos"> 
  <p class="nome">{{ info.dados.nome }}</p>
  <p class="email">{{ info.dados.email }}</p>
  <p class="user">{{ info.dados.user }}</p>
  <p class="trabalho">{{ info.dados.trabalho }}</p>
  <p class="cidade">{{ info.dados.cidade }}</p>
  <div class="erro"> 
  <p v-if="info.erro" class="erro">Id não encontrado</p>
</div>
</div>

</div>
</template>
<style scoped>

</style>
