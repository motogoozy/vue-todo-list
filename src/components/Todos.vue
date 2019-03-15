<template>
   <div>
      <div v-bind:key="todo.id" v-for="todo in todos"> <!-- receiving props and iterating through them -->
         <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" /> <!-- v-bind is passing the individual todo as props to the TodoItem component. v-on is catching the delete event from the TodoItem component-->
      </div>
   </div>
</template>

<script>
import TodoItem from "./TodoItem.vue"

export default {
   name: "Todos",
   components: {
      TodoItem
   }, 
   props: ["todos"] //accepting the todos props from App.vue as an array. We iterate through this array with v-for in the div above
}
</script>j

<style scoped>

</style>
