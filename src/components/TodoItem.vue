<template>
    <div class="inserir-texto">
        <InputText v-model="description" id="texto"></InputText>
    </div>
    <div class="div-botoes">
        <Button @click="cancel" id="btn-voltar" label="info" class="p-button-outlined">Voltar</Button>
        <Button @click="saveTodo" id="btn-salvar" label="info" class="p-button-outlined">Salvar</Button>

    </div>

    
  </template>
  
  <script>
  
  
  export default {
    data() {
        return {
            description: ""
        }
    },
    props:{
        todo: Object

    },

    created(){
        if(this.todo){
            this.description=this.todo.description;
        }

    },
    methods:{
        cancel(){
            this.$emit("cancel");
        },
        saveTodo(){
            this.$emit("saveTodo", { ...this.todo, description: this.description});
        }
    }
    
  }
  
  </script>
  
  <style scoped>
  
  .div-botoes{
    margin-top: 1rem;
  }
    
  #btn-voltar{
    margin-right: 1rem;
    padding: 15px;
    border-radius: 10px;
  }

  #btn-salvar{
    padding: 15px;
    border-radius: 10px;
  }

  .inserir-texto{
    display:inline-flexbox;
    align-items:center;
    margin-top: 20px;

  }

  #texto{
    width: 80%;
  }

  </style>