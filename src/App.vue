<template>
  <Dna v-bind:items="items"/>
</template>

<script>
import Dna from './components/Dna.vue'
export default {
  name: 'App',
  components: {
    Dna
  },
  data() {
        return {
            items: [
              {id: 1, title: 'title', content: 'content'},
              {id: 2, title: 'title', content: 'content'},
              {id: 3, title: 'title', content: 'content'},
              {id: 4, title: 'title', content: 'content'}
            ]
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
