<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: "todas",
  tarefa_cadastro: "",
  tarefas: [
    {
      titulo: "Estudar Vue e React",
      finalizada: false
    },
    {
      titulo: "Aprender mais sobre o fetch do js",
      finalizada: false
    },
    {
      titulo: "Trocar ssd do thinkpad",
      finalizada: true
    }
  ]
})

const pegarTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const pegarTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const pegarTarefasFiltradas = () => {
  const filtro = estado.filtro

  switch (filtro) {
    case "pendentes":
      return pegarTarefasPendentes()
    case "finalizadas":
      return pegarTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastrarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefa_cadastro,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefa_cadastro = ""
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ pegarTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefa_cadastro" @change="event => estado.tarefa_cadastro = event.target.value" required class="form-control" type="text" placeholder="Descrição da tarefa">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Adicionar</button>
        </div>
        <div class="col-md-2">
          <select @change="event => estado.filtro = event.target.value" class="form-control">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in pegarTarefasFiltradas()">
        <input @change="event => tarefa.finalizada = event.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
