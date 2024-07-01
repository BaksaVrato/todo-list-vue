<template>
<div class="relative">
  <div
    class="flex items-center p-4 rounded gap-4 bg-gray-100 mb-3"
    :class="{ 'bg-gray-300': item.isDone, 'text-gray-500' : item.isDone}"
  >
    <p class="flex flex-1 text-lg font-semibold">{{ item.text }}</p>

    <div 
      class="flex gap-2 text-xl v-if"
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
    </div>

      <!-- TODO - vyrolluj aditional text, po pridani je vyrolovane, vies vyrolovat viac naraz -->
  </div>

  <!-- TODO - lepsie pls -->
  <div 
      v-if="item.isDone"
      class="absolute w-[90%] h-1 bg-black bottom-7 z-10 opacity-50 left-1/2 -translate-x-1/2"
      :class="{'cross' : item.isDone }"
    >    
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

  const removeItem = () => {
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

</script>

<style scoped>
.cross {
  animation: cross 1s ease-in-out;
}

@keyframes cross {
  0% {
    width: 0%;
  }
  100% {
    width: 90%;
  }
}



</style>