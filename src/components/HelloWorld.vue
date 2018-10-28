<template>
  <div id="todo">
    <ol>
      <li v-for="todo in todos"> {{todo.title}} {{todo.completed}} <button @click="handleTodos(todo)">Done</button></li>
    </ol>
  </div>
</template>

<script>

export default {
  name: 'todo',
  props:['todos'],
  components: {
  },
  methods:{
    handleTodos(todo){
      this.$emit('doneTodo', todo)
    }
  },
  data(){
    return {

    }
  }
}
</script>

<style>

</style>
