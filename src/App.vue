<template>
  <div id="app">
    <auto-complete :persons="persons" field="name"></auto-complete>
  </div>
</template>

<script>
import persons from './person-data';
import AutoComplete from './components/auto-complete.vue';

export default {
  name: 'App',
  components: {
    AutoComplete
  },
  data() {
    return {
      persons
    };
  }
};
</script>
