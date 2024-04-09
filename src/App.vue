<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input type="text" v-model="newTask" placeholder="Ajouter une nouvelle tâche">
    <button @click="addTask">+</button>
    <br>
    <span class="error">{{ errorMessage }}</span>

    <TableTask v-if="tasks.length > 0" :tasks="tasks" @delete-task="deleteTask" @edit-task="editTask"/>
    <p v-else>Aucune tâche en cours.</p> 
    <!-- <button @click="seeTasks()" >voir les taches</button> -->

  </div>
</template>

<script>
import TableTask from './components/TableTask.vue'

export default {
  name: 'App',
  components: {
    TableTask
  },
  data() {
    return {
      title: 'Ma toDo List',
      newTask: '',
      tasks: [],
      errorMessage: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTask.length >= 3) {
        this.tasks.push({ title: this.newTask, completed: false });
        this.newTask = '';
        this.errorMessage = '';
      } else {
        this.errorMessage = 'La tâche doit contenir au moins 3 caractères.';
      }
    },

    deleteTask(task) {
      alert(task.title + ' va être supprimer, êtes-vous sûr ?')
      const index = this.tasks.indexOf(task);
      if (index > -1) {
        this.tasks.splice(index, 1);
      }
    },

    editTask(task) {
      console.log(task);
      const index = this.tasks.indexOf(task);
      if (index > -1) {
        let newTitle = prompt('Modifier la tâche', this.tasks[index].title);
        while (newTitle && newTitle.length < 3 ) {
          newTitle = prompt('Le titre de la tâche doit comporter au moins 3 caractères. Veuillez réessayer.', this.tasks[index].title);
        }
        if (newTitle) {
          this.tasks[index].title = newTitle;
        }
      }
    },

    // seeTasks() {
    //   console.log(this.tasks);
    // }
    
  },

}
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

.error {
  color: red;
  font-size: smaller;
  font-style: italic;
}
input{
  margin: 10px;
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
button {
  padding: 8px 15px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #f0f0f0;
  cursor: pointer;
}
</style>
