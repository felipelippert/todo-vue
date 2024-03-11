<script setup>
  import { reactive } from 'vue';
  import Header from './components/Header.vue'
  import Form from './components/Form.vue'
  import TodoList from './components/TodoList.vue'

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
        completed: true,
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
    <Header :pendingTasks="getPendingTasks().lenght"/>
    <Form :changeFilter="event => state.filter = event.target.value" :tempTask="state.tempTask" :editTempTask="event => state.tempTask = event.target.value" :addTask="addTask" />
    <TodoList :tasks="getFilteredTasks()" /> 
  </div>
</template>
