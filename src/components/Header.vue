<script setup>
  const props = defineProps(['tarefasPendentes']);
</script>

<template>
  <header class="p-5 mb-4 mt-4 bg-light-subtle rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
      Você possui <strong>{{ props.tarefasPendentes }}</strong> tarefas pendentes
    </p>
  </header>
  </template>
