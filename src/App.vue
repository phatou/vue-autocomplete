<template>
  <div id="app">
    <auto-complete :persons="persons" field="name"></auto-complete>
  </div>
</template>

<script>
import AutoComplete from './components/auto-complete.vue';

export default {
  name: 'App',
  components: {
    AutoComplete
  },
  data() {
    return {
      persons: [
        { id: 2, name: 'Jeff', age: 32 },
        { id: 1, name: 'Paul', age: 24 },
        { id: 3, name: 'Gwen', age: 27 }
      ]
    };
  }
};
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
