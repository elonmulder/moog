<template>
  <div id="app">
    <dial max="1000"></dial>
  </div>
</template>

<script>
import components from './components';

export default {
  name: 'app',

  components,

  data() {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>

</style>
