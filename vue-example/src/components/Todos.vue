<template>
  <div id="todos" class="jumbotron">
    <div>
      <h3>Todos</h3>
      <hr>
      <h5>Total: {{ todosSize }}</h5>
    </div>
    <div v-for="todo in todos" :key="todo.id">
      <h4>{{ todo.name }}</h4>
      <button class="btn btn-primary" v-on:click="removeTodo(todo)">Remove</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "todos",
  props: ['todos'],
  methods: {
    removeTodo (todo) {
      this.$emit('evtRemoveTodo', todo);
    }
  },
  computed: {
    todosSize () {
      return this.todos.length;
    }
  }
}
</script>

<style scoped>
</style>
