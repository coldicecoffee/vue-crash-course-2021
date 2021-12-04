<template>
  <header class="header">
    <h1>{{ title }}</h1>
    <Button text="Add Task" color="green" />
    <!-- <Button text="Update Task" color="red" />
    <Button text="Remove Task" color="blue" /> -->
  </header>
</template>

<script>
import Button from "./Button";

export default {
  name: "Header",
  props: {
    title: String,
  },
  components: {
    Button,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
}
</style>
