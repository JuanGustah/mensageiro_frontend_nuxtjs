<template>
  <div>
    <H1>Usuários do sistema mensageiro</H1>
    <div>
      <ul>
        <li v-for="usuario in listaUsuarios" :key="usuario.id">
          {{usuario.email}} - {{usuario.nome}}
        </li>
      </ul>
    </div>
    <div><button v-on:click="carregarListagemUsuarios">Atualizar</button></div>
  </div>
  <RouterLink to="adicionarUsuario">Cadastrar novo usuário</RouterLink>
</template>

<script setup>
  import MensageiroService from '../service/MensageiroService'
  import { onMounted, ref } from 'vue'

  const listaUsuarios = ref([]);

  function carregarListagemUsuarios() {
    MensageiroService.list().then(
      response => {
        listaUsuarios.value = response.data;
        console.log('Listagem recebida com sucesso');
      })
      .catch(error => {
        console.error('Erro ao receber listagem:', error);
      });
  }

  onMounted(
    () => { carregarListagemUsuarios(); }
  )
</script>
