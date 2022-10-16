<template>
  <TaskComponent/>
</template>

<script>
import TaskComponent from './components/TaskComponent.vue'

export default {
  name: 'App',
  components: {
    TaskComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-size: 14px;
}
</style>
