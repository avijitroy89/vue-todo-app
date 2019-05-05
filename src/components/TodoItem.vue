<template>
  <p v-bind:class="{'is-selected':todo.completed}" >
    <input type="checkbox" v-on:change="checkTodos" v-model="todo.completed">
    {{todo.title}}
    <button v-on:click="$emit('del-todo', todo.id)">X</button>
    </p>
  
</template>
<script>
export default {
  name: "TodoItem",
  props:["todo"],
  methods: {
    checkTodos () {
      // console.log(this.todo.completed)
      this.todo.completed = !this.todo.completed
    }
  }
};
</script>
<style scoped>
.is-selected {
  text-decoration: line-through;
}
</style>
