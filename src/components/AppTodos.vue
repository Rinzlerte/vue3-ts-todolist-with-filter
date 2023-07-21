<template>
      <ul class="todo-list">
        <!-- single usage -->
        <!-- <AppTodoLIstItem 
            :todo="{id:0, text: 'hello 11', isCompleted: true}"
        /> -->
        <AppTodoLIstItem 
            v-for="todo in todos" 
            :key="todo.id" 
            :todo="todo" 
            @toggle-todo="toggleTodo"
            @remove-todo="remove"
        />
        </ul>
</template>

<script lang="ts">

import {PropType, defineComponent} from 'vue';
import AppTodoLIstItem from './AppTodoLIstItem.vue'
import {Todo} from '@/types/Todo'

export default defineComponent({
  components: {
    AppTodoLIstItem
  },
  props: {
    todos: Array as PropType<Todo[]>
  },
  methods: {
    toggleTodo(id: number | string): void{
      this.$emit('toggleTodo', id)
    },
    remove(id: number | string): void{
      this.$emit('toggleTodo', id)
    }
  },
  emits: {
    toggleTodo: ( id: number | string) => id,
    removeTodo: ( id: number | string) => id,
  }
})


</script>