<template>
  <div
    class="flex items-center p-4 rounded gap-4 bg-gray-100 mb-3"
  >
    <p class="flex flex-1">{{ text }}</p>
    <div class="flex gap-2 text-xl">
      <i class="fa-regular fa-trash-can hover:cursor-pointer"></i>
      <i class="fa-regular fa-circle-check hover:cursor-pointer"></i>
    </div>
</div>
</template>

<script setup>
  import { defineProps, ref } from 'vue'

  const text = ref('Sample textample textample textample textample textample textample text...')

  const props = defineProps({
    text: String
  })
</script>
