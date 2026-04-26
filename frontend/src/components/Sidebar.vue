<script>
import SidebarLink from './SidebarLink.vue';
import { collapsed, toggleSidebar, sidebarWidth } from './state'

export default {
  props: {},
  components: { SidebarLink },
  setup() {
    return { collapsed, toggleSidebar, sidebarWidth }
  }
}
</script>

<template>
  <div class="sidebar" :style="{ width: sidebarWidth }">
    <div class="sidebar-header">
      <h1 class="sidebar-title">
        <span v-if="collapsed">DMR</span>
        <span v-else>Demorô</span>
      </h1>
    </div>

    <nav class="sidebar-nav">
      <SidebarLink to="/dashboard"  icon="fas fa-tachometer-alt">Dashboard</SidebarLink>
      <SidebarLink to="/login"      icon="fas fa-sign-in-alt">Realizar Login</SidebarLink>
      <SidebarLink to="/register"   icon="fas fa-user-plus">Realizar Registro</SidebarLink>
      <SidebarLink to="/amigos"     icon="fas fa-users">Ver Amigos</SidebarLink>
      <SidebarLink to="/posts"      icon="fas fa-pencil-alt">Escreva algo</SidebarLink>
    </nav>

    <span
      class="collapse-icon"
      :class="{ 'rotate-180': collapsed }"
      @click="toggleSidebar"
    >
      <font-awesome-icon icon="fa-solid fa-angle-double-left" />
    </span>
  </div>
</template>

<style scoped>
.sidebar {
  margin: 0;
  padding: 0;
  background-color: #ffffff;
  border-right: 1px solid #dddfe2;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.05);
  color: #1d2129;
  position: fixed;
  height: 100%;
  overflow: hidden;
  transition: width 0.3s ease;
  display: flex;
  flex-direction: column;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

.sidebar-header {
  padding: 24px 20px 16px;
  border-bottom: 1px solid #dddfe2;
}

.sidebar-title {
  margin: 0;
  font-size: 1.3em;
  font-weight: 700;
  color: #007bff;
  white-space: nowrap;
  overflow: hidden;
}

.sidebar-nav {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 12px 0;
  gap: 4px;
}

.collapse-icon {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 14px 0;
  display: flex;
  justify-content: center;
  color: #aaa;
  cursor: pointer;
  border-top: 1px solid #dddfe2;
  transition: color 0.2s, background-color 0.2s;
}

.collapse-icon:hover {
  color: #007bff;
  background-color: #f0f2f5;
}

.rotate-180 {
  transform: rotate(180deg);
  transition: 0.2s linear;
}
</style>