<template>
   <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
      <input type="checkbox" v-on:change="markComplete ">
      <p>{{todo.title}}</p>
      <button @click="$emit('del-todo', todo.id )" class="del">x</button> <!-- del-todo is the name of the event listener, todo.id is a parameter that is being passed up to the deleteTodo function in App.vue  -->
   </div>
</template>

<script>
export default {
   name: "TodoItem",
   props: ["todo"],
   methods: {
      markComplete() {
         this.todo.completed = !this.todo.completed;
      }
   }
}
</script>

<style scoped>
   .todo-item {
      background: #f4f4f4;
      padding: 10px;
      border-bottom: 1px #ccc dotted;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
   }

   .is-complete {
      text-decoration: line-through;
   }

   .del {
      background: #ff0000;
      color: #fff;
      border: none;
      padding: 5px 9px;
      border-radius: 50%;
      cursor: pointer;
   }
</style>
