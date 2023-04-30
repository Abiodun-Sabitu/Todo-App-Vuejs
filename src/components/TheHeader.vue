<template>
  <header class="container-fluid text-center py-5">
    <h2>{{ headerTitle }}<i class="fa-solid fa-rocket fs-5 ms-1"></i></h2>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      headerTitle: "Todo App",
    };
  },
};
</script>

<style scoped>
header {
  background-color: #caf0f8;
}
h2 {
  font-weight: 800;
  color: #0077b6;
}
</style>
