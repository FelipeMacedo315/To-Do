<template>
  <div id="app">
    <div id="search-form">
      <input
        v-bind:value="textTask"
        v-on:change="captureTxtSearch"
        type="search"
      />
      <button v-on:click="sendTxtCard">+</button>
    </div>
    <div id="container-all-cards" v-if="textTaskCard">
      <Task v-bind:contentTask="textTaskCard" />
    </div>
    <div v-else></div>
  </div>
</template>

<script>
import Task from "./components/Task.vue";
export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      textTask: "",
      textTaskCard: [],
    };
  },
  methods: {
    captureTxtSearch(event) {
      this.textTask = event.target.value;
    },
    sendTxtCard() {
      this.textTask.length > 0 ? this.textTaskCard.push(this.textTask) : null;
      this.textTask = "";
    },
  },
};
</script>

<style>
html {
  height: 100%;
}
body {
  height: 100%;
}
#app {
  padding: 0%;
  margin: 0%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  gap: 20px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}
#container-all-cards {
  width: 100%;
}
#search-form {
  display: flex;
  width: 30%;
}
input {
  width: 100%;
  padding: 5px;
}
</style>
