<template>
<div class="relative">
  <div
    class="flex items-center p-4 rounded gap-4 bg-gray-100 mb-3"
    :class="{ 'bg-gray-300 duration-1000': item.isDone, 'text-gray-500' : item.isDone , 'opacity-0 duration-300': removed}"
  >
    <p class="flex flex-1 text-lg font-semibold">{{ item.text }}</p>

    <div 
      class="flex gap-2 text-xl"
    >
      <i 
        class="fa-regular fa-trash-can hover:cursor-pointer"
        @click="removeItem"
      >del</i>
      <i 
        v-if="!item.isDone" 
        class="fa-regular fa-circle-check hover:cursor-pointer"
        @click="itemDone"
      >done</i>
      <i 
        class="fa-solid fa-eye hover:cursor-pointer"
        @click="viewItem"
      >view</i>
      <i
        class="hover:cursor-pointer"
        @click="rollItem"
      > <!-- add icon -->
        roll
      </i>
    </div>

    <div
      v-if="isRolled"
    >
      <p>asdasdasda asd asd asd asd asd</p>
  </div>

  </div>
  
</div>

</template>

<script setup>
  import { defineProps, ref } from 'vue'

  import { useRouter } from 'vue-router';

  const router = useRouter();

  const viewItem = () => {
    router.push({ name: 'item', params: { id: props.item.id }});
  }

  const props = defineProps({
    item: {
      type: Object,
      default: {}
    }
  });

  const emit = defineEmits(['remove-item']);

  const removed = ref(false);
  const removeItem = async () => {
    removed.value = true;

    await new Promise((resolve) => setTimeout(resolve, 500));

    emit('remove-item', props.item.id);
  }

  const itemDone = () => {
    props.item.isDone = true;
    let itemList = JSON.parse(localStorage.getItem('itemList'));
    itemList = itemList.map(item => {
      if(item.id === props.item.id) {
        item.isDone = true;
      }
      return item;
    })
    localStorage.setItem('itemList', JSON.stringify(itemList));
  }

  const isRolled = ref(false);
  const rollItem = () => {
    isRolled.value = !isRolled.value;
  }

</script>

<style scoped>

</style>