<template>
  <div class="home">
    <tasks-list v-if="$store.state.tasks.length" />
    <no-tasks v-else />
    <button-done-sorting v-if="$store.state.sorting"/>
  </div>
</template>

<script>
import TasksList from '../components/Todo/TasksList.vue'
import NoTasks from '../components/Todo/NoTasks.vue'
import ButtonDoneSorting from '../components/Todo/ButtonDoneSorting.vue'

  export default {
    name: 'Todo',
    components: {
      'tasks-list': TasksList,
      'no-tasks': NoTasks,
      'button-done-sorting': ButtonDoneSorting
    }
  }
</script>