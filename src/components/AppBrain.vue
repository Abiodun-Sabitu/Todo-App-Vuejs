<template>
  <the-header></the-header>
  <todo-creator></todo-creator>
</template>
<script>
import TheHeader from "./TheHeader.vue";
import TodoCreator from "./TodoCreator.vue";
export default {
  components: {
    TheHeader,
    TodoCreator,
  },
  data() {
    return {};
  },
};
</script>
<style></style>
