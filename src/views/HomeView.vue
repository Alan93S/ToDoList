<template>


  <h1 class="font">To Do List</h1>
  <input type="text" placeholder="Ingresar tarea" v-model="taskNameToAdd" />
  <button type="button" @click="addNewTask">Agregar</button>
  <div>

    <div>

      <p class="font"> Con esta sencilla, pero util aplicación realizada con VUEJS, podrás agregar las tareas que tengas pendientes por hacer al mismo tiempo que puedes ir borrando aquellas que ya realizaste. ¡Pruebalo ya!</p>

    </div>

    <h3 class="font">Listado</h3>
    <div class="todo-row" v-for="task of taskList" :key="task.name">
      {{ task.name }}
      <button type="button" @click="deleteTask(task.id)">delete</button>
    </div>
  </div>


</template>

<script>
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      taskNameToAdd: "",
      taskList: [],
    };
  },
  methods: {
    addNewTask() {
      let newTaskToAdd;
      if (this.taskNameToAdd !== "") {
        newTaskToAdd = {
          id: Math.floor(Math.random() * 100),
          name: this.taskNameToAdd,
        };
        this.taskList = [...this.taskList, newTaskToAdd];
      }
    },
    deleteTask(id) {
      this.taskList = this.taskList.filter((task) => task.id !== id);
    },
  },
  watch: {
    taskList: {
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.taskList));
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      this.taskList = JSON.parse(localStorage.getItem("tasks"));
    } else {
      this.taskList = [];
    }
  },
};
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@300&display=swap');

.todo-row {
  background-color: gray;
  width: 500px;
  margin: 0 auto;
  color:white;
  font-size: 20px;
  font-family: 'Roboto Condensed', sans-serif;

}

body {

  background-color: rgb(0, 0, 0);
 
}

.font {

  color: white;
  font-family: 'Roboto Condensed', sans-serif;
}

</style>
