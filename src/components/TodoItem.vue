<template>
  <li :class="{ completed: todo.complete , editing:editing}">
    <div class="view">
      <input type="checkbox" class="toggle" v-model="isTodoCompleted" />
      <label for="" @dblclick="startediting()">{{ todo.title }}</label>
      <button class="destroy" @click="emit('delete-todo',todo)"></button>
    </div>
    <div class="input-container">
      <input type="text" id="edit-to-input" class="edit" v-model="editInput">
      <label for="edit-to-input" class="hiden"> Editer </label>
    </div>
  </li>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { computed, ref } from 'vue'
const props = defineProps<{
  todo: Todo
}>()

const editing = ref<boolean>(false)


const emit = defineEmits<{
  (e: 'delete-todo', todo: Todo): void
  (e: 'update-todo', todo: Todo, completedVal): void
}>()


function startediting(){
  editing.value = true
}
//une version avancé de la notion de computed
//
const isTodoCompleted = computed({
  get: () => props.todo,
  set: (newVal: boolean) => emit('update-todo', props.todo, newVal)
})


const editText = ref<string>("")
const editInput = computed({
  get: () => props.todo.title,
  set: (val) => { editText.value = val }
})


</script>

<style scoped></style>
