<template>
  <main class="main">
    <ul class="todo-list">
      <TodoItem 
      v-for="todo in taches" 
      :key="todo.id" 
      :todo="todo"  
      @delete-todo="emit('delete-todo',todo)"
      @update-todo="updateTodo" />
    </ul>
  </main>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import TodoItem from '@/components/TodoItem.vue'
// const props = defineProps(['taches']);

const props = defineProps<{
  taches: Todo[]
}>()

function updateTodo(todo:Todo,completedVal:boolean){
  emit('update-todo',todo,completedVal)
}
const emit = defineEmits<{
  (e:'delete-todo',todo:Todo):void
  (e:'update-todo',todo:Todo, completedVal):void
}>()

</script>

<style scoped></style>
