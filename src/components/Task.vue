<template>
  <div :class="[task.reminder ? 'reminder' : '', 'task']">
    <div class="wrapper">
      <h3>{{ task.text }}</h3>
      <button @click="onDelete(task.id)">remove</button>
    </div>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      this.$emit("delete-task", id);
    },
  },
};
</script>

<style scoped>
.task {
  background: #f4f4f4;
  margin: 15px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.task .wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task button {
  cursor: pointer;
}
</style>