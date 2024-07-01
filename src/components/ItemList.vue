<template>
  <ItemAdder @add-item="addItemToList"/>
  <div v-for="item in itemList" :key="item">
    <Item :item="item" @remove-item="removeItem"/>
  </div>
</template>

<script setup>
  import Item from '@/components/Item.vue'
  import ItemAdder from '@/components/ItemAdder.vue'
  import { ref } from 'vue';
  import { uid } from 'uid';

  const itemList = ref([
    {
      id: uid(),
      text: 'Sample textample textample textample textample textample textample text...',
      isDone: false
    },
    {
      id: uid(),
      text: 'Sample textample textample textample textample textample textample text...',
      isDone: true
    }
  ])

  const addItemToList = (text) => {
    itemList.value.push({
      id: uid(),
      text: text,
      isDone: false
    }) 
    console.log(itemList.value);
    }

  const removeItem = (id) => {
    itemList.value = itemList.value.filter(item => item.id !== id)
  }

</script>

