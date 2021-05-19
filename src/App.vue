<template>
  <List />
</template>

<script>
  import List from './views/List.vue';

  export default {
    name: 'App',
    components: {
      List
    },
  }
</script>

<style>
  html {
    font-family: Arial, Helvetica, sans-serif;
  }

  button {
    background-color: transparent;
    outline: none;
    border: 1px solid #aaa;
    border-radius: 3px;

    transition: background-color .1s ease-in-out;
  }

  input {
    border: 1px solid #aaa;
    border-radius: 3px;
  }

  button:active {
    transition: none;
    background-color: #00ff88;
  }
</style>