<template>
  <li :class="{ completed: todo.complete }">
    <div class="view">
      <input type="checkbox" class="toggle" v-model="isTodoCompleted"/>
      <label for="">{{ todo.title }}</label>
      <button class="destroy" @click="emit('delete-todo',todo)"></button>
    </div>
  </li>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { computed } from 'vue'
const props = defineProps<{
  todo: Todo
}>()

const emit = defineEmits<{
  (e:'delete-todo',todo:Todo):void
  (e:'update-todo',todo:Todo, completedVal):void
}>()

//une version avancé de la notion de computed
//
const isTodoCompleted = computed({
  get:()=>props.todo,
  set:(newVal: boolean)=> emit('update-todo',props.todo , newVal)
})
</script>

<style scoped></style>
