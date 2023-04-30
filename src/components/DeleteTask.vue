<template>
  <span>
    <i
      class="fa-solid fa-trash-can me-3 mt-2 mutate-icons text-danger"
      @click="deleteItem"
    ></i>
  </span>
</template>

<script>
export default {
  emits: ["delete-task"],
  methods: {
    deleteItem() {
      this.$emit("delete-task");
    },
  },
};
</script>

<style>
.mutate-icons {
  cursor: pointer;
}
</style>
