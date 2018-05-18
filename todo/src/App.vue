<template>
  <div id="app">
    <todoHead></todoHead>
    <todo></todo>
    <todoFoot></todoFoot>
  </div>
</template>

<script>
  import TodoHead from './components/todoHead';
  import TodoFoot from './components/todoFoot';
  import Todo from './components/todo.vue';
  export default {
    name: 'App',
    components: {
      TodoHead,
      TodoFoot,
      Todo
    }
  }
</script>

<style>
*{ margin: 0; padding: 0; list-style: none; }
input, input:focus{ border: none; outline: none; }
html,body{ width: 100%; height: 100%; }
body{ background: url(./assets/banner.jpg); font-family: 'Avenir', Helvetica, Arial, sans-serif; }
#app {
  width: 100%; height: 100%; background-color: rgba(255,255,255,0.3);
}
</style>
