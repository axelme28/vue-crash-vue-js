<template>
  <header class="d-flex justify-content-between mb-3">
    <h1 class="text-center">{{ title }}</h1>
    <Button
      :textButton="showAddTask ? 'close' : 'addTask'"
      :color="showAddTask ? '#f7ca20' : '#007358'"
      @toggle-add-task="$emit('toggle-add-task')"
    />
  </header>
</template>

<script>
import Button from './Button.vue';
import Tasks from './Tasks.vue';
export default {
  name: 'Header',
  components: {
    Button,
    Tasks,
  },
  emits: ['toggle-add-task'],
  props: {
    title: {
      type: String,
      default: 'default value',
    },
    showAddTask: Boolean,
  },
  //   props: ["title"],
  //   props: {
  //     title: String,
  //   },
};
</script>

<!-- scope significa que la logica de estilos se queda en este componente -->
<style scope></style>
