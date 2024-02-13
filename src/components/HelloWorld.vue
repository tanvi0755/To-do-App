<template>
  <div class="container">
    <h1 class="my-4">My To-Do List</h1>

    <div class="input-group mb-3">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Add a new task..."
        class="form-control"
      />
      <button @click="addTask" class="btn btn-primary">Add</button>
    </div>

    <ul class="list-group">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        class="list-group-item"
      >
        <div class="d-flex justify-content-between align-items-center">
          <span :class="{ 'completed-task': task.completed }">{{ task.text }}</span>
          <button
            @click="toggleTaskStatus(index)"
            class="btn btn-success btn-sm"
          >
            {{ task.completed ? 'Mark Incomplete' : 'Mark Complete' }}
          </button>
        </div>
      </li>
    </ul>

    <div class="mt-4">
      <h2>Filter Tasks</h2>
      <button @click="filterTasks('all')" class="btn btn-secondary mx-1">All</button>
      <button @click="filterTasks('active')" class="btn btn-secondary mx-1">Active</button>
      <button @click="filterTasks('completed')" class="btn btn-secondary mx-1">Completed</button>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';

export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'all',
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    toggleTaskStatus(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    filterTasks(type) {
      this.filter = type;
    },
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'all') {
        return this.tasks;
      } else if (this.filter === 'active') {
        return this.tasks.filter(task => !task.completed);
      } else if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      }
      return this.tasks;
    },
  },
};
</script>

<style scoped>
.completed-task {
  text-decoration: line-through;
}
</style>
