<template>
  <div id="todo">
    <ol>
      <li v-for="todo in todos"> {{todo}}</li>
    </ol>
  </div>
</template>

<script>

export default {
  name: 'todo',
  props:['todos'],
  components: {

  },
  data(){
    return {

    }
  }
}
</script>

<style>

</style>
