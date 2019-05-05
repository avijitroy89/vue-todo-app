<template>
  <div id="app">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" name="avijit"/> -->
    <todos v-bind:todos="toDos" v-on:del-todo="deltodo"/>
    <Addtodo v-on:addtodo="addtodo"/>
  </div>
</template>

<script>
import axios from "axios";
import uuid from "uuid";
import HelloWorld from '../components/HelloWorld.vue';
import Todos from '../components/Todos.vue';
import Addtodo from '../components/Addtodo.vue';


export default {
  name: 'home',
  components: {
    Todos,
    Addtodo
  },
  data(){
    return{
      toDos: []
    }
  },
  methods:{
    deltodo (id){  console.log(id)    
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`) 
      .then(res => this.toDos = this.toDos.filter((e) => {
        return e.id != id 
      }))
      .catch(err=>console.log(err))
      
    },
    addtodo (todo){
      let newTodo = {
        title: todo,
        completed: false
      }
      axios.post("https://jsonplaceholder.typicode.com/todos", newTodo) 
      .then(res => {
        this.toDos = [...this.toDos,res.data],
        console.log(res.data)
        })
      .catch(err=>console.log(err))
      
    }
  },
  mounted: function(){
      axios.get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => this.toDos = res.data)
      .catch(err=>console.log(err))
    },
  updated: function(){
    console.log('update')
  },
  destroyed: function(){
    console.log('delete')
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
