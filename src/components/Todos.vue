<template>
  <div>
    <div v-if="todos.length > 0">
      <div class="form-text text-muted text-center" style="font-style: italic !important;">Double click to toggle status</div>
      <ul v-for="todo in todos" :key="todo.id">
        <Todo   
            @toggle-completed="$emit('toggle-completed', todo.id)"  
            @delete-todo="$emit('delete-todo', todo.id)" 
            @edit-todo="$emit('edit-todo', todo)"
            :todo="todo"
          />
      </ul>
      
    </div>
    <div v-else>
      No todo to show
    </div>

  </div>

</template>

<script>

import Todo from './Todo.vue'

export default {
  name: 'Todos',
  props: {
    todos: Array,
  },
  components: {
    Todo
  },
  emits: ['delete-todo', 'toggle-completed', 'edit-todo']
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
