<template>
  <Dna/>
</template>

<script>
import Dna from './components/Dna.vue'
export default {
  name: 'App',
  components: {
    Dna
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
