<template>
  <Header title="Test Tracker" />
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld
    msg="Welcome to Your Vue.js App"
    customMsg="This is my custom message!"
  />
</template>

<script>
import Header from "./components/Header.vue";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    Header,
    HelloWorld,
  },
  data() {
    return {
      tasks: [],
    };
  },
  created() {
    this.tasks = [
      { id: 1, text: "Doc Appointment", day: "March 1st at 2:30 pm", reminder: true },
      { id: 2, text: "Meeting at School", day: "April 4th at 12:30 pm", reminder: true },
      { id: 3, text: "Having a lunch with colleagues", day: "June 23rd at 6:00 pm", reminder: false },
      { id: 4, text: "Going home at the moment", day: "July 24th at 8:30 pm", reminder: true },
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
