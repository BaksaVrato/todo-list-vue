<template>
  <div>
    <SiteNavbar/>
    <router-view/>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import SiteNavbar from '@/components/SiteNavbar.vue';
</script>
