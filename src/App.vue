<template>
  <div class="app">
    <Home />
  </div>
</template>

<script>
import Home from './views/Home';

export default {
  components: {
    Home,
  }
}
</script>


<style lang="scss">
  * {
    box-sizing: border-box;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
  }
</style>
