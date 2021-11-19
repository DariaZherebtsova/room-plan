<template>
  <div id="app">
    <div class="room">
      <Plan />
      <Legend />
    </div>
    
  </div>
</template>

<script>
import Plan from './components/Plan.vue';
import Legend from './components/Legend.vue'

export default {
  name: 'App',
  components: {
    Plan,
    Legend,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  box-sizing: border-box;
}

.room {
  display: grid;
  grid-template-columns: 1fr 320px;
  border: 1px solid var(--light-grey);
  max-width: 1000px;
  height: 100%;
  margin: 0 auto;
}
</style>
