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
      todos:[{
      "id": 1,
      "title": "walk dog",
      "completed": false
      },
      {
      "id": 2,
      "title": "clean room",
      "completed": false
      },
      {
      "id": 3,
      "title": "get gas",
      "completed": false
      }]
    }
  }
}
</script>

<style>

</style>
