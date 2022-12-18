<template>
    <div class="todo-list">
        <div v-for="(todo, index) in todos" :key="index" class="todo-item">
        <label class="todo-label">
            {{todo.description}}
        </label>
        <Button icon="pi pi-pencil" class="p-button-rounded p-button-text"
        @click="$emit('editTodo',index)"></Button> 
        <Button icon="pi pi-trash" class="p-button-rounded p-button-text" 
        @click="$emit('deleteTodo',index)"></Button> 
        </div>
    </div>
        </template>
  
  <script>
  
  
  export default {
    props: {
        todos: Array
    }
    
  }
  
  </script>
  
  <style scoped>
  .todo-list{
    margin: 1rem;
  }

  .todo-item{
    display: flex;
    align-items:center;
    border: 1.5px solid rgba(9, 75, 243, 0.12);
    text-align: left;
    padding-left: 10px;
    margin-left: 20px;
    margin-right: 20px;
    background-color: rgb(253, 251, 251);
    border-radius: 10px;
  }
    
  .todo-label{
    flex-grow: 1;

  }
  
  </style>