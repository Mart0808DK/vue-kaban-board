<template>
  <div>
    <NavBar/>
    <div class="flex justify-center ">
      <div class="min-h-screen flex overflow-x-scroll py-12">
        <KabanBoard/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import KabanBoard from './components/KabanBoard.vue';
import NavBar from './components/NavBar.vue';

export default defineComponent({
  name: 'App',
  components: {
    KabanBoard,
    NavBar

  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
