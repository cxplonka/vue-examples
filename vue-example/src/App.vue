<template>
  <div id="app">
    <!-- bind event to method and bind computed property -->
    <tasks v-on:evtTaskAdded="taskAdded" v-bind:tasks="nonAddedTasks"></tasks>
    <todos v-on:evtRemoveTodo="removeTodo" v-bind:todos="todos"></todos>
  </div>
</template>

<script>
import Tasks from './components/Tasks'
import Todos from './components/Todos'

export default {
  name: 'App',
  data () {
    return {
      todos: [],
      tasks: [
        {id: 0, name: 'Task 1', added: false},
        {id: 1, name: 'Task 2', added: false},
        {id: 2, name: 'Task 3', added: false}
      ]
    }
  },
  computed: {
    nonAddedTasks() {
      return this.tasks.filter((task) => {
        return !task.added;
      });
    }
  },
  methods: {
    // event from tasks
    taskAdded (task) {
      this.todos.push({id: task.id, name: 'Todo ' + task.id});
    },
    // event from todos
    removeTodo (todo) {
      const task = this.tasks.find(task => {
        return task.id == todo.id;
      });
      task.added = false;
      this.todos.splice(this.todos.indexOf(todo), 1);
    }
  },
  components: {
    Tasks, Todos
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
