<template>
  <AddTask v-if="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import AddTask from "../components/AddTask.vue";
import Tasks from "../components/Tasks.vue";

export default {
  name: "Home",
  components: {
    AddTask,
    Tasks,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);

      fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
          headers: {
            "Content-type": "application/json",
          },
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting a task");
      }
    },
    async fetchTasks() {
      const response = await fetch("api/tasks");
      const data = await response.json();
      return data;
    },
    async fetchTask(id) {
      const response = await fetch(`api/tasks/${id}`);
      const data = await response.json();
      return data;
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updateTask),
      });
      const data = await res.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
