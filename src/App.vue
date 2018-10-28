<template>
  <div id="app">
    <HelloWorld @doneTodo="doneTodo" :todos="todos" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  methods:{
    doneTodo(todo){
      todo.completed = !todo.completed
    }
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
