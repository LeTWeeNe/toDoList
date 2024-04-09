<template>
    <div class="tableWithFilters">
        <select v-model="filter">
            <option value="all">Toute les tâches</option>
            <option value="completed">Tâches complétées</option>
            <option value="not-completed">Tâches non complétées</option>
        </select>
        <table>
        <tr v-for="task in filteredTasks" :key="task.title" >
            <td>
            <TodoTask :task="task" @delete-task="deleteTask" @edit-task="editTask"/>
                
                
            </td>
        </tr>
        </table>
    </div>
  </template>
  
  <script>
  import TodoTask from './TodoTask.vue'
  
  export default {
    name: 'TableTask',
    components: {
      TodoTask
    },
    props: ['tasks'],
    data() {
        return {
        filter: 'all'
        }
    },
    methods: {
        deleteTask(task) {
            this.$emit('delete-task', task);
        },

        editTask(task) {
            this.$emit('edit-task', task);
        }
        
    },
    computed: {
        filteredTasks() {
            if (this.filter === 'completed') {
                return this.tasks.filter(task => task.completed);
            } else if (this.filter === 'not-completed') {
                return this.tasks.filter(task => !task.completed);
            } else {
                return this.tasks;
            }
        }
    },
  }
  </script>

<style>
table {
    margin: 0 auto;
    border-collapse: collapse;
    width: 50%;    
  }
  
td {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: left;
}
select {
    margin: 0 auto;
    padding: 8px;
    border: 1px solid #ccc;
    border-bottom: none;
    cursor: pointer;
    width: 50%;
}
.tableWithFilters {
    display: flex;
    flex-direction: column;
    margin-top: 50px;
}



</style>