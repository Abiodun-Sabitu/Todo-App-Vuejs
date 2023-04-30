<template>
  <span
    ><i
      class="fa-solid fa-pen-to-square mt-2 mutate-icons text-mute"
      @click="editItem"
    ></i
  ></span>
</template>

<script>
export default {
  emits: ["edit-task"],
  methods: {
    editItem() {
      this.$emit("edit-task");
    },
  },
};
</script>

<style></style>
