<template>
  <ItemAdder @add-item="addItemToList"/>
  <div v-for="item in itemList" :key="item">
    <ItemCard :item="item" @remove-item="removeItem"/>
  </div>
</template>

<script setup>
  import ItemCard from '@/components/ItemCard.vue'
  import ItemAdder from '@/components/ItemAdder.vue'
  import { ref } from 'vue';
  import { uid } from 'uid';

  const itemList = ref([])
  if(localStorage.getItem('itemList')) {
    itemList.value = JSON.parse(localStorage.getItem('itemList'));
  }

  const addItemToList = (text) => {
    itemList.value.push({
      id: uid(),
      text: text,
      isDone: false,
      aditionalInfo: ''
    }) 
    console.log(itemList.value);
    localStorage.setItem('itemList', JSON.stringify(itemList.value));
    console.log(localStorage.getItem('itemList'));
    }

  const removeItem = (id) => {
    itemList.value = itemList.value.filter(item => item.id !== id)
    localStorage.setItem('itemList', JSON.stringify(itemList.value));
  }

</script>

