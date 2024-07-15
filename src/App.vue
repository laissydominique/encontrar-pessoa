<script setup>
import { ref } from "vue";

const info = ref({
  id: null,
  dados: " ",
  erro: false,
});

async function teste() {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/users/${info.value.id}`
  );
  const data = await response.json();
  console.log(data);

  info.value.dados = {
    nome: data.name,
    tel: data.phone,
    email: data.email,
    user: data.username,
  };

  if (!data.id) {
    info.value.erro = true;
  }
}
</script>

<template>
  <input v-model="info.id" type="text" />
  <button @click="teste"></button>

  <p class="nome">{{ info.dados.nome }}</p>
  <p class="tel">{{ info.dados.tel }}</p>
  <p class="email">{{ info.dados.email }}</p>
  <p class="user">{{ info.dados.user }}</p>

  <p v-if="info.erro" class="erro">Id não encontrado</p>
</template>

<style scoped>
button {
  width: 70px;
  height: 20px;
}
</style>
