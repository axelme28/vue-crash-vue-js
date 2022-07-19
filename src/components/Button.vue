<template>
  <button class="btn text-white" :style="{ backgroundColor: color }" @click="handleClick()">
    {{ textButton }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    textButton: {
      type: String,
      default: "button",
    },
    color: {
      type: String,
      default: "white",
    },
  },
  methods: {
    handleClick() {
      this.$emit("toggle-add-task");
    },
  },

  //   comments: {},
};
</script>
