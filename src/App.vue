<script setup>
import { reactive } from 'vue';


  const state = reactive({
    filter: 'all',
    tempTask: '',
    tasks: [
      {
        title: 'Study ES6',
        completed: false,
      },
      {
        title: 'Study Vue.js',
        completed: false,
      },
      {
        title: 'Go to the gym',
        completed: true
      }
    ]
  })

  const getPendingTasks = () => {
    return state.tasks.filter(task => !task.completed)
  }
  const getCompletedTasks = () => {
    return state.tasks.filter(task => task.completed)
  }

  const getFilteredTasks = () => {
    const { filter } = state;

    switch (filter) {
      case 'pending':
        return getPendingTasks();
      case 'completed':
        return getCompletedTasks();
      default:
        return state.tasks;
    }
  }

  const addTask = () => {
    const newTask = {
      title: state.tempTask,
      completed: false,
    }
    state.tasks.push(newTask);
    state.tempTask = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rouded-3">
      <h1>My tasks:</h1>
      <p>
        You have {{ getPendingTasks().lenght }} pending tasks.
      </p>
    </header>
    <form @submit.prevent="addTask">
      <div class="row">
        <div class="col">
          <input :value="state.tempTask" @change="event => state.tempTask = event.target.value" required class="form-control" type="text" placeholder="Type task description here">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Register</button>
        </div>
        <div class="col-md-2">
          <select @change="event => state.filter = event.target.value" class="form-control">
            <option value="all">All tasks</option>
            <option value="pending">Pending tasks</option>
            <option value="completed">Completed tasks</option>
          </select>
        </div>
      </div>
    </form>
    {{ state.filter }}
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input @change="event => task.completed = event.target.checked" :checked="task.completed" :id="task.title" type="checkbox">
        <label :class="{ done: task.completed}" class="ms-3" :for="task.title">
          {{ task.title }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
