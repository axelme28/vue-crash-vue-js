<template>
  <form class="w-50 shadow-lg rounded p-5" @submit="handleNewTask">
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">Text</label>
      <!-- prettier-ignore -->
      <input type="text" class="form-control" placeholder="text" name="text" v-model="text">
    </div>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">Day</label>
      <!-- prettier-ignore -->
      <input type="text" class="form-control" placeholder="day" name="day" v-model="day">
    </div>
    <div class="mb-3 form-check">
      <input type="checkbox" class="form-check-input" id="exampleCheck1" v-model="reminder" />
      <label class="form-check-label" for="exampleCheck1">Set reminder</label>
    </div>
    <button type="submit" class="btn btn-primary">Save task</button>
  </form>
</template>

<script>
import Swal from "sweetalert2";
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    handleNewTask(e) {
      e.preventDefault();
      if (!this.text || !this.day) {
        Swal.fire({
          icon: "error",
          title: "Oops...",
          text: "Text and day are required",
        });
        return;
      }
      const newTask = {
        id: Math.floor(Math.random() * 100),
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };
      this.$emit("add-task", newTask);

      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scope></style>
