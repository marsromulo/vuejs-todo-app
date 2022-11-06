<template>
  <div class="container w-50 mt-4">
    <Header />
    <AddTodo @add-todo="addTodo" @update-todo="updateTodo" :idToEdit="idToEdit" :titleToEdit="titleToEdit"  />
    <Todos @toggle-completed="toggleCompleted"  @delete-todo="deleteTodo" @edit-todo="editTodo" :todos="todos"  />
    <ClearTodo @clear-todo="clearTodo" />
  </div>
</template>

<script>
import axios from 'axios'
import Todos from './components/Todos'
import Header from './components/Header'
import AddTodo from './components/AddTodo'
import ClearTodo  from './components/ClearTodo'

export default {
  name: "App",
  components: {
    Todos,
    Header,
    AddTodo,
    ClearTodo
  },
  data() {
    return {
      todos: [],
      titleToEdit:"",
      idToEdit:null

    }
  },
  methods: {

     addTodo(newTodo){
      this.todos = [newTodo, ...this.todos]
    }, 

    deleteTodo(id){
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },

    toggleCompleted(id){
      this.todos = this.todos.map(
        (todo) => todo.id === id ? {...todo, completed: !todo.completed} : todo 
      )
    },

    editTodo(todo){
      this.titleToEdit=todo.title;
      this.idToEdit=todo.id;
      console.log(todo.title);
    },

    updateTodo({id,title}){
      this.todos = this.todos.map(
        (todo) => todo.id === id ? {...todo, title: title} : todo 
      )
      this.titleToEdit = "";
      this.idToEdit = null;
    },
    clearTodo(){
      this.todos = []
    },

    async fetchTodos(){
      const res  = await axios.get('https://jsonplaceholder.typicode.com/todos');
      const data = res.data;
      return data;
    }
   
  },

async created() {
    this.todos = await this.fetchTodos();
  }
}

</script>
