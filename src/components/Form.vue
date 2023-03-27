<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaCadastro', 'editarCadastro', 'trocarFiltro']);
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaCadastro" @change="props.editarTarefa" required class="form-control" type="text" placeholder="Descrição da tarefa">
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Adicionar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
