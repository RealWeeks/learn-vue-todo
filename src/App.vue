<template>
  <div id="app">
    <h2 v-if="todoChange">Todo Has changed</h2>
    <HelloWorld @doneTodo="doneTodo" :todos="todos" />

    Todos Done:
    <ul>
      <li v-for="todo in todosDone">{{todo.title}}</li>
    </ul>
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
  watch:{
    todosDone(){
      this.todoChange = true
      setTimeout(()=>{
        this.todoChange = false
      }, 2000)
    }
  },
  computed:{
    todosDone(){
      return this.todos.filter(x => x.completed)
    }
  },
  data(){
    return {
      todoChange:false,
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
