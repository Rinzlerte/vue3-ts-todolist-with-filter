<template>
     <aside class="app-filters">
        <section class="toggle-group">
          <button 
            v-for="filter in filters" 
            :key="filter" 
            class='button'
            :class="{'button--primary' : activeFilter === filter}"
            @click="setFilter(filter)"
          >
            {{filter}}
          </button>
          <!-- <button class='button' :class="{'button--primary' : activeFilter === 'All'}">All</button>
          <button class='button' :class="{'button--primary' : activeFilter === 'Active'}">Active</button>
          <button class='button' :class="{'button--primary' : activeFilter === 'Done'}">Done</button> -->
        </section>
      </aside>
</template>

<script lang="ts">

import { defineComponent , PropType} from 'vue';
import {FilterType} from '@/types/Filter'

interface State {
  filters : FilterType[]
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<FilterType>,
      required: true
    }
  },
  data(): State{
    return {
      filters: ['All', 'Active', 'Done']
    }
  },
  methods: {
    setFilter(filter : FilterType){
      this.$emit('setFilter', filter)
    }
  },
  emits: {
    setFilter: (filter : FilterType) => filter
  }
})

</script>