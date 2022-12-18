<template>

  <h1>LISTA DO MEU AMOR JESSICA ABBADIA, </h1>
  <h2> PARA ORGANIZAR A VIAGEM PARA DISNEY</h2>
  <img id="fogos" src="./img/fogos.png">
  <img id="castelo" src="./img/castelo.png">
  <img id="fogos" src="./img/fogos.png" alt="" srcset="">

  <div v-if="!editMode">
    <Button id="btn-tarefa" @click="newTodo"  label="info" class="p-button-outlined">Nova Tarefa</Button>
    <todo-list :todos="todos" @deleteTodo="deleteTodo" @editTodo="editTodo"></todo-list>
  </div>
<todo-Item v-if="editMode" @cancel="cancel" @saveTodo="saveTodo" :todo="todo"></todo-Item>
<footer>Feito por Marcelo Abbadia</footer>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TodoItem from "./components/TodoItem.vue";


export default {
  components:{
    TodoList,
    TodoItem
  },
  data(){
    return{
      editMode:false,
      todos:[],
      todo: null,
      nextId:1,
    }

  },
  methods:{
    newTodo(){
      this.todo = null;
      this.editMode = true;
    },
    cancel(){
      this.editMode =false;

    },
    saveTodo(todo){
      if(todo.id){
        const index= this.todos.findIndex((item)=> item.id === todo.id);
        this.todos[index]=todo;
      } else {
        todo = { id: this.nextId, ...todo };
        this.todos.push(todo);
        
        this.nextId++;
        localStorage.setItem("nextId", this.nextId);
      }
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.editMode =false;
    },
    deleteTodo(index){
      this.todos.splice(index,1);
      localStorage.setItem("todos",JSON.stringify(this.todos));

    },
    editTodo(index){
      this.todo =this.todos[index];
      this.editMode=true;

    }

  },
  created(){
   const todos = localStorage.getItem("todos");
   if (todos){
    this.todos =JSON.parse(todos);
   }
   const nextId = localStorage.getItem("nextId");
   if(nextId){
    this.nextId=parseInt(nextId);
     }
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Comfortaa&family=Nunito:ital,wght@0,200;1,200&display=swap');

#app {
  font-family: 'Comfortaa', cursive;
  color: #2c3e50;
  
}


h1{
  margin-top: 50px;
  color:rgb(65, 145, 243);
  text-align: center;
}

h2{
color:rgb(65, 145, 243);
text-align: center;
}


body{
background-color: rgba(17, 255, 227, 0.135);
color:rgb(9, 75, 243);
text-align: center;


}

#btn-tarefa{
  margin-top: 10px;
  padding: 20px;
  border-radius: 10px;
}

#castelo{
  width: 200px;
}

#fogos{
  width: 250px;
  
}

footer{
  font-size: 10px;
  margin-top: 20%;
}

</style>

