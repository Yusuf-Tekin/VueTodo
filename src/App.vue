<template>
  <Todo />
</template>

<script>
import Todo from './components/Todo.vue';

export default {
  name: 'App',
  components: {
    Todo
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #F5EEDC;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
