<script>
  let id = 0  

  export default{
    
    
    data(){
      return {
        newToDo : '',
        todolist: [
          {id: id++, text: 'Learn Vue'},
          {id: id++, text: 'Learn Vue1'}
        ]
      }
    },

    methods: {
      addToDo(){
        this.todolist.push({id: id++, text: this.newToDo});
        this.newToDo = '';
      },
      
      removeToDo(todo){
        this.todolist = this.todolist.filter(task => task != todo);
      }

    }
  }
</script>

<template>
  <form @submit.prevent="addToDo">
    <input v-model="newToDo">
    <button type="submit"> Add toDo</button>
  </form>

  <ul>
    <li v-for="todo in todolist">
      {{todo.text}}
      <button @click="removeToDo(todo)"> Remove </button>
    </li>
  </ul>
</template>

<style>
  .title{
    color: red;
  }
</style>