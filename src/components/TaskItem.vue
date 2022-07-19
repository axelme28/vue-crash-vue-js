<template>
  <!-- prettier-ignore -->
  <div @dblclick="$emit('toggle-reminder',task.id)" :class="[task.reminder ? 'task-reminder' : '', 'alert shadow-lg rounded']">
    <div class="d-flex justify-content-end">
      <button class="btn btn-danger" @click="$emit('delete-task',task.id)">Delete</button>
    </div>
    <h4>{{ task.text }}</h4>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    task: {
      type: Object,
      default: "this is a task",
    },
  },
};
</script>
<style scope>
.task-reminder {
  border-left: 5px solid green;
}
.alert {
  cursor: pointer !important;
}
</style>
