<template>
  <div 
    class="container flex flex-col mx-auto"
  >
    <ItemAdder/>
    <TodoItemList/>
    <hr>
    <DoneItemList/>
  </div>
</template>

<script setup>
  import ItemAdder from '@/components/ItemAdder.vue'
  import TodoItemList from '@/components/TodoItemList.vue'
  import DoneItemList from '@/components/DoneItemList.vue'
  import { ref } from 'vue'
 
</script>
