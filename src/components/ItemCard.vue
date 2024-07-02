<template>
<div 
  class="relative"
  :class="{'opacity-0 duration-300': removed}"
  >
  <div
    class="flex items-center p-4 rounded-t gap-4 bg-gray-100"
    :class="{ 'bg-gray-300 duration-1000': item.isDone, 'text-gray-500' : item.isDone , 'mb-3 rounded-b': !isRolled }"
  >
    <p class="flex flex-1 text-lg font-semibold">{{ item.text }}</p>

    <div 
      class="flex gap-2 text-xl items-center"
    >
      <i 
        class="fa-regular fa-trash-can hover:cursor-pointer"
        @click="removeItem"
      ></i>
      <i 
        v-if="!item.isDone" 
        class="fa-regular fa-circle-check hover:cursor-pointer"
        @click="itemDone"
      ></i>
      <i 
        class="fa-solid fa-eye hover:cursor-pointer"
        @click="viewItem"
      ></i>
      <i
        class="hover:cursor-pointer fa-solid fa-caret-down"
        @click="rollItem"
        v-if="!item.isDone" 
      >
      </i>
    </div>
  </div>
  <div
      v-if="isRolled"
      class="flex flex-col p-4 rounded-b bg-gray-50 mb-3 text-sm"
    >

<!-- TODO saving to localStorage -->

      <p>Aditional notes:</p>
      <p v-if="!isEditing">{{ item.aditionalInfo }}</p>
      <input 
        type="text" 
        placeholder="Additional notes" 
        class="bg-white"
        v-model="item.aditionalInfo"
        v-else
      />
      <i @click="toggleEdit" class="fa-solid fa-pen-to-square hover:cursor-pointer"></i>
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

  const isEditing = ref(false);
  const toggleEdit = () => {
    isEditing.value = !isEditing.value;
  }

</script>

<style scoped>

</style>