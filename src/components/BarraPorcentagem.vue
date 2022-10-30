<template>
  <div id="barra-porcentagem-container">
    <h1>Tarefas</h1>
    <div id="barra-porcentagem">
      <span> {{ calculeValuePorcentagem().toFixed(0) }}% </span>
      <div v-bind:style="{ width: calculeValuePorcentagem() + '%' }" id="barra-progress"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["allTasks"],
  methods: {
    calculeValuePorcentagem() {
      const value = this.allTasks.filter((item) => {
        return item.complete === true;
      });
      return Math.round((value.length / this.allTasks.length) * 100 || 0);
    },
  },
};
</script>

<style scoped>
* {
  color: white;
}
#barra-porcentagem-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
h1 {
  line-height: 10%;
}
#barra-porcentagem {
  width: 80%;
  border: groove white 2px;
  border-radius: 10px;
  position: relative;
  display: flex;
  flex-direction: column;
}
#barra-progress {
  border: none;
  border-radius: inherit;
  position: absolute;
  background-color: rgb(39, 184, 39);
  height: 100%;
  align-self: flex-start;
}
span {
  z-index: 1;
}
</style>
