<script>
import { RouterView } from 'vue-router'
import Sidebar from './components/Sidebar.vue'
import { sidebarWidth } from './components/state'

export default {
  components: { Sidebar },
  setup() {
    return { sidebarWidth }
  }
}
</script>

<template>
  <Sidebar />

  <main class="main-content" :style="{ 'margin-left': sidebarWidth }">
    <RouterView />
  </main>
</template>

<style>
.main-content {
  transition: margin-left 0.3s ease-in-out;
}
</style>