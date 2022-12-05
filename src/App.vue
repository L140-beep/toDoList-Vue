<script>
  let id = 0  

  export default{
    
    
    data(){
      return {
        newToDo : '',
        todolist: [
          {id: id++, text: 'Learn Vue', done: false},
          {id: id++, text: 'Learn Vue1', done: false}
        ],
        helper: "",
        hideCompleted: false
      }
    },

    methods: {
      addToDo(){
        if (!this.newToDo){
          this.helper = "Empty string!"
        }
        else{
          this.helper = ""
          this.todolist.push({id: id++, text: this.newToDo, done: false});
          this.newToDo = '';
        }
      },
      
      removeToDo(todo){
        this.todolist = this.todolist.filter(task => task != todo);
      }
    },

    computed: {
      filtredToDos(){
        if(this.hideCompleted){
          return this.todolist.filter(todo => todo.done == false)
        }
        
        return this.todolist
      }
    }
  }
</script>

<template>
  <form @submit.prevent="addToDo">
    <input v-model="newToDo" placeholder="new toDo...">
    <button type> Add toDo</button>
    
    <div v-if="helper">
      {{helper}}
    </div>

  </form>

   <ul>
    <li v-for="todo in filtredToDos">
      <input type="checkbox" v-model="todo.done">
      <span :class="{done : todo.done}">{{todo.text}} </span>
      <button @click="removeToDo(todo)"> X </button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{hideCompleted ? "Show all" : "Hide completed"}}
  </button>
</template>

<style>
  .title{
    color: red;
  }

  .done{
    text-decoration: line-through;
  }
</style>