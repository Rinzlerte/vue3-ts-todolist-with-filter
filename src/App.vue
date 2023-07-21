<template>
  <AppHeader/>
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter"/>
  <main class="app-main">
    <AppTodos 
      :todos="filteredTodos" 
      @toggle-todo="toggleTodo" 
      @remove-todo="remove"

    />
    <AppAddTodo @add-todo="addTodo"  />
  </main>
  <AppFooter :stats="stats"/>
</template>

<script lang="ts">

import {Todo} from '@/types/Todo'
import {defineComponent} from 'vue';
import AppHeader from './components/AppHeader.vue'
import AppFilters from './components/AppFilters.vue'
import AppTodos from './components/AppTodos.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFooter from './components/AppFooter.vue'
import {FilterType} from '@/types/Filter'
import {Stats} from '@/types/Stats'


interface todoState {
  todos: Todo[],
  activeFilter: FilterType
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodos,
    AppAddTodo,
    AppFooter
  },
  data(): todoState {
    return {
        todos: [
            {
              id: 0, text: 'vue todos app', isCompleted: true
            },
            {
              id: 1, text: 'vue some basics app', isCompleted: false
            },
            {
              id: "3", text: 'vue filter list', isCompleted: false
            }
        ],
        activeFilter: 'All'
    }
  },
  // properties and logic
  computed: {
    filteredTodos(): Todo[]{
        switch(this.activeFilter){
          case 'Active':
            return this.activeTodos
          case 'Done':
            return this.doneTodos
          case 'All':
          default :
            return this.todos
        }
    },
    stats(): Stats {
      return {
          activeTasks : this.activeTodos.length,
          tasksDone: this.doneTodos.length
      }
    },
    activeTodos(): Todo[]{
      return this.todos.filter( todo => !todo.isCompleted)
    },
    doneTodos():  Todo[]{
      return this.todos.filter( todo => todo.isCompleted)
    }
  },
  methods: {
    toggleTodo(id: number | string): void{
      const targetTodo = this.todos.find((todo : Todo)=> todo.id === id);
      if (targetTodo) {
        targetTodo.isCompleted = !targetTodo.isCompleted
      }
    },
    remove(id: number | string): void{
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    },
    addTodo(todo: Todo){
      // this.todos.push(todo);
      this.todos = [todo, ...this.todos]
    },
    setFilter(filter: FilterType) {
      this.activeFilter = filter;
    }
  }
})
</script>