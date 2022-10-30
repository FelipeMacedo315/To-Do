<template>
  <div id="all-cards">
    <section
      v-bind:class="contentTask[index].complete ? 'card-task-completed' : 'card-task-incompleted'"
      v-bind:key="index"
      v-for="(task, index) in contentTask"
      @dblclick="changeStatusTask(index)"
    >
      <div class="close-icon">
        <img v-on:click="deleteTask(index)" src="../assets/icons8-close-64.png" alt="close-icon" />
      </div>
      <p>{{ task.task }}</p>
    </section>
  </div>
</template>

<script>
export default {
  props: ["contentTask"],
  data() {
    return {
      taskStatusClass: false,
    };
  },

  methods: {
    deleteTask(index) {
      this.contentTask.splice(index, 1);
    },
    changeStatusTask(indexCard) {
      this.contentTask[indexCard].complete = !this.contentTask[indexCard].complete;
    },
  },
  watch: {
    contentTask: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.contentTask));
      },
    },
  },
};
</script>

<style scoped>
#all-cards {
  width: 100%;
  display: grid;
  grid-template-columns: 25% 25% 25%;
  grid-column-gap: 10%;
  grid-row-gap: 15%;
}
.card-task-incompleted {
  border-radius: 10px;
  background-color: brown;
  color: white;
  width: 100%;
  padding: 20px;
  user-select: none;
}
.card-task-completed {
  border-radius: 10px;
  background-color: rgb(39, 184, 39);
  color: white;
  font-weight: bolder;
  text-decoration: line-through black;
  width: 100%;
  padding: 20px;
  user-select: none;
}
.close-icon {
  display: flex;
  justify-content: flex-end;
}
.close-icon img {
  height: 15px;
}
@media (max-width: 768px) {
  #all-cards {
    padding: 0% 10%;
    display: grid;
    grid-template-columns: 70%;
    grid-row-gap: 10%;
  }
}
</style>
