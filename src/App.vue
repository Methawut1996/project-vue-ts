<template>
  <Navbar />
  <!-- <sidebar /> -->
  <div><router-view /></div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Navbar from "@/components/Navbar.vue"; 
import Sidebar from "@/components/sidebar.vue";

export default defineComponent({
  components: {
    Navbar,
    Sidebar,
  },
});
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt:wght@200;300;400;500;600;700;800;900&display=swap');
#app {
  font-family: Prompt, Helvetica, Arial, sans-serif;
  text-align: center;
}


</style>
