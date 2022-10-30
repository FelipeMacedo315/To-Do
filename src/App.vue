<template>
  <div id="app">
    <BarraPorcentagem v-bind:allTasks="textTaskCard" />
    <div id="search-form">
      <input
        placeholder="Nova Tarefa ?"
        v-bind:value="textTask"
        v-on:change="captureTxtSearch"
        type="text"
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
import BarraPorcentagem from "./components/BarraPorcentagem.vue";
export default {
  name: "App",
  components: {
    Task,
    BarraPorcentagem,
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
      this.textTask.length > 0
        ? this.textTaskCard.push({ task: this.textTask, complete: false })
        : null;
      this.textTask = "";
      localStorage.setItem("tasks", JSON.stringify(this.textTaskCard));
    },
  },
  created() {
    const localTasks = JSON.parse(localStorage.getItem("tasks"));
    console.log(localTasks);
    this.textTaskCard.push(...localTasks);
  },
};
</script>

<style>
html {
  height: 100%;
}
body {
  height: 100%;
  background-color: #2c3e50;
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
  justify-content: space-evenly;
  width: 40%;
}
input {
  color: white;
  width: 95%;
  padding: 5px;
  background-color: transparent;
  outline-style: none;
  border: 1px solid white;
  font-size: 1em;
}
button {
  font-size: 1.5em;
  min-width: 5%;
  background-color: #00a8ff;
  color: white;
  border: none;
  border: 1px solid white;
}
@media (max-width: 768px) {
  #app {
    gap: 30px;
  }
  #search-form {
    width: 90%;
  }
  button {
    width: 10%;
  }
}
</style>
