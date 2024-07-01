<!-- worst component name ever -->
<template>
  <div
    class="flex py-4 px-8 gap-4"
  >
    <input 
      type="text" 
      placeholder="Add new item" 
      class="w-full text-xl bg-gray-300 p-3 "
      v-model="text"
    />
    <button
      class="w-16 bg-gray-300 hover:bg-gray-400 font-semibold py-2 px-4 rounded shadow"
      @click="addItem()"
    >
      Add
    </button>
  </div>
</template>

<script setup>
  import { ref, defineEmits } from 'vue'


  const text = ref('');

  const emit = defineEmits(['add-item']);
  const addItem = () => {

    if(text.value === '') return;
    
    emit('add-item', text.value);
    text.value = '';
  }

</script>
