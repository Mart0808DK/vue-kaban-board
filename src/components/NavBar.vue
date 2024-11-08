<template>
  <div class="navbar flex justify-between items-center p-4 bg-gray-800 text-white fixed w-full top-0 left-0 z-50">
    <div class="navbar-left">
      <h1 class="text-xl font-bold">KabanBoard</h1>
    </div>
    <div class="navbar-right flex items-center">
      <img src="../assets/photo.jpg" alt="Martin Emil Nielsen" class="w-10 h-10 rounded-full mr-6"/>
      <h1 class="text-xl font-bold">Martin Emil Nielsen</h1>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'NavBar'
});
</script>

<style scoped>
</style>