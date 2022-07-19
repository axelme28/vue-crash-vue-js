<template>
  <div class="p-5 main-view">
    <Header
      title="Task tracker"
      @toggle-add-task="handleToggleAddTask"
      :showAddTask="showAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="handleAddTask" />
    </div>
    <Tasks :tasks="tasks" @delete-task="handleDeleteTask" @toggle-reminder="handleToggleReminder" />
  </div>
</template>

<script>
import Swal from 'sweetalert2';

import AddTask from './components/AddTask.vue';
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  async created() {
    this.tasks = await this.getTasks();
  },
  methods: {
    async getTasks() {
      const response = await fetch('http://localhost:5000/tasks');
      const data = await response.json();
      return data;
    },
    async getSingleTask(id) {
      const response = await fetch(`http://localhost:5000/tasks/${id}`);
      const data = await response.json();
      return data;
    },
    handleDeleteTask(id) {
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!',
      }).then((result) => {
        if (result.isConfirmed) {
          fetch(`http://localhost:5000/tasks/${id}`, {
            method: 'DELETE',
            headers: {
              Accept: 'application/json',
              'Content-Type': 'application/json',
            },
          }).then(() => {
            Swal.fire('Deleted!', 'Your file has been deleted.', 'success');
            this.tasks = this.tasks.filter((task) => task.id !== id);
          });
        }
      });
    },
    async handleToggleReminder(id) {
      const currentTask = await this.getSingleTask(id);
      const updatedTask = { ...currentTask, reminder: !currentTask.reminder };

      const response = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'content-type': 'application/json',
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await response.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async handleAddTask(task) {
      const response = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task),
      });
      const data = await response.json();

      this.tasks = [...this.tasks, data];
    },
    handleToggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
  },
};
</script>

<style>
.main-view {
  background-color: #f4f6f6;
}
</style>
