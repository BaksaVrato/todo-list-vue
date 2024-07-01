<template>
  <div
    class="flex items-center p-4 rounded gap-4 bg-gray-100 mb-3"
    :class="{ 'bg-gray-300': item.isDone, 'text-gray-500' : item.isDone }"
  >
    <p class="flex flex-1 text-lg font-semibold">{{ item.text }}</p>

    <div 
      class="flex gap-2 text-xl v-if"
    >
      <i 
        class="fa-regular fa-trash-can hover:cursor-pointer"
        @click="$emit('remove-item', item.id)"
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
    console.log("removal")
    emit('remove-item', props.item.id);
  }

  const itemDone = () => {
    props.item.isDone = true;
  }

</script>
