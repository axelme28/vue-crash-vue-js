<template v-for="item in tasks">
  <div class="mt-5">
    <div class="location-item" v-for="item in tasks.slice().reverse()" :key="item.id">
      <!-- <p>{{ item.text }}</p> -->
      <TaskItem
        :task="item"
        @delete-task="$emit('delete-task', item.id)"
        @toggle-reminder="$emit('toggle-reminder', item.id)"
      />
    </div>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";
export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },
  components: {
    TaskItem,
  },
  emits: ["delete-task", "toggle-reminder"],
};
</script>
