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
  <input  v-model="info.id" type="text" placeholder="Digite ID aqui" />
  <button @click="teste"></button>

  <p class="nome">{{ info.dados.nome }}</p>
  <p class="email">{{ info.dados.email }}</p>
  <p class="user">{{ info.dados.user }}</p>
  <p class="trabalho">{{ info.dados.trabalho }}</p>
  <p class="cidade">{{ info.dados.cidade }}</p>


  

  <p v-if="info.erro" class="erro">Id não encontrado</p>
</template>

<style scoped>

</style>
