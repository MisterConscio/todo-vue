<script setup>
import { reactive } from 'vue';
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import Todolist from './components/Todolist.vue'

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
    <Header :tarefas-pendentes="pegarTarefasPendentes().length"/>
    <Form
      :tarefa-cadastro="estado.tarefa_cadastro"
      :editar-cadastro="event => estado.tarefa_cadastro = event.target.value"
      :cadastrar-tarefa="cadastrarTarefa"
      :trocar-filtro="event => estado.filtro = event.target.value"
    />
    <Todolist :tarefas-filtradas="pegarTarefasFiltradas()"/>
  </div>
</template>

