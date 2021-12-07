<template>
  <Header
    @toggle-add-task="toggleAddTask"
    title="Test Tracker"
    :showAddTask="showAddTask"
  />
  <AddTask v-if="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import AddTask from "./components/AddTask.vue";
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";

export default {
  name: "App",
  components: {
    AddTask,
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
    },
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doc Appointment",
        day: "March 1st at 2:30 pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Meeting at School",
        day: "April 4th at 12:30 pm",
        reminder: true,
      },
      {
        id: 3,
        text: "Having a lunch with colleagues",
        day: "June 23rd at 6:00 pm",
        reminder: false,
      },
      {
        id: 4,
        text: "Going home at the moment",
        day: "July 24th at 8:30 pm",
        reminder: true,
      },
    ];
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
