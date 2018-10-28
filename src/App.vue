<template>
  <div id="app">
    <HelloWorld :todos="todos" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data(){
    return {
      todos:['shopping', 'get gas', 'walk dog']
    }
  }
}
</script>

<style>

</style>
