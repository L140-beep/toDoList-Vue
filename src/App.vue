<script>

  let id = 0  

  export default{
    
    
    data(){
      return {
        newToDo : '',
        todolist: [],
        helper: "",
        hideCompleted: false
      }
    },

    mounted(){
      if (localStorage.getItem('todolist')){
        this.todolist = JSON.parse(localStorage.getItem('todolist'));
      }
    }, 

    watch: {
      todolist: {
        handler(new_list, old_list){
          const parsed = JSON.stringify(new_list)
          console.log('New list = ', parsed)
          localStorage.setItem('todolist', parsed)
        },
        deep: true
      },
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
      },

      clear(){
        localStorage.setItem('todolist', JSON.stringify([]))
      },
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

  <button @click="clear">
    Clear
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