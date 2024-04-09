<template>
    
    <div class="task">
        <div>
            <input type="checkbox" v-model="localTask.completed">
            <span :class="{ 'is-completed': localTask.completed }">{{ localTask.title }}</span>
        </div>
        <div class="buttons">
            <button @click="deleteTask">supprimer</button>
            <button @click="editTask" :disabled="localTask.completed">modifier</button>
        </div>
    </div>
    
</template>
  
  <script>
  export default {
    name: 'TodoTask',
    props: ['task'],
    data() {
      return {
        localTask: this.task
      }
    },
    watch: {
      task(newVal) {
        this.localTask = newVal;
      }
    },
    methods: {
        deleteTask() {
            this.$emit('delete-task', this.localTask);
        },
        
        editTask() {
            this.$emit('edit-task', this.localTask);
        }
    }
  }
  </script>
  
  <style>
  .is-completed {
    text-decoration: line-through;
  }
  .buttons {
    display: flex;
    gap: 5px;
    }
    .task {
        display: flex;
        justify-content: space-between;
        
    }
    button {
        padding: 8px 15px;
        border-radius: 5px;
        border: 1px solid #ccc;
        background-color: #f0f0f0;
        cursor: pointer;
    }
    :disabled {
        background-color: #ccc;
        cursor: not-allowed;
    }
    
    
  </style>