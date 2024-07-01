<template>
  <!-- TODO -->
  <div>
    <h1>{{ itemData.text }}</h1>
    <p>{{ itemData.aditionalInfo }}</p>
    <p>{{ itemData.isDone }}</p>
    <p>{{ itemData.id }}</p>
  </div>
</template>

<script setup>

  import { ref } from 'vue'
  import { useRoute } from 'vue-router'

  const route = useRoute();
  const itemData = ref(JSON.parse(localStorage.getItem('itemList')).find(item => item.id === route.params.id));
  console.log('data: ' + itemData.value.text);

</script>