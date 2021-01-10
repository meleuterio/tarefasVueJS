<template>
  <div id="app">
    <header>Minhas Tarefas</header>
    <task/>
    <div class="rodape">
      <span> 2021 &copy; </span>
    </div>
  </div>
</template>

<script>
import Task from './components/Task'

export default {
  name: 'App',
  components: {
    Task
  }
}
</script>

<style scoped>
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 80px;
    font-size: 40px;
    color: #FBFAF8;
  }

  .rodape {
    color: #FBFAF8;
    text-align: right;
    margin-top: 50px;
    margin-right: 50px;
    font-size: 12px;
  }
</style>
