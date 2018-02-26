<template>
  <div id="tasks">
    <h3>Tasks</h3>
    <hr>
    <div class="jumbotron" v-for="task in tasks" :key="task.id">
      <h4>{{ task.name }}</h4>
      <button class="btn btn-primary" v-on:click="addTask(task)">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "tasks",
  props: ['tasks'],
  methods: {
    addTask(task) {
      this.$emit('evtTaskAdded', task);
      task.added = true;
    }
  }
}
</script>

<style scoped>
</style>
