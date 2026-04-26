<script>
import { computed } from 'vue'
import { useRoute } from 'vue-router';
import { collapsed } from './state';

export default {
  props: {
    to:   { type: String, required: true },
    icon: { type: String, required: true }
  },
  setup(props) {
    const route = useRoute()
    const isActive = computed(() => route.path === props.to)
    return { isActive, collapsed }
  }
}
</script>

<template>
  <router-link :to="to" class="link" :class="{ active: isActive }">
    <font-awesome-icon :icon="icon" class="icon" />
    <transition name="fade">
      <span v-if="!collapsed">
        <slot />
      </span>
    </transition>
  </router-link>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.1s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.link {
  display: flex;
  align-items: center;
  cursor: pointer;
  position: relative;
  font-weight: 500;
  font-size: 0.95em;
  user-select: none;
  margin: 2px 8px;
  padding: 10px 12px;
  border-radius: 8px;
  height: auto;
  color: #4b4f56;
  text-decoration: none;
  transition: background-color 0.2s, color 0.2s;
}

.link:hover {
  background-color: #f0f2f5;
  color: #1d2129;
}

.link.active {
  background-color: #e7f1ff;
  color: #007bff;
  font-weight: 600;
}

.link .icon {
  flex-shrink: 0;
  width: 20px;
  margin-right: 10px;
  font-size: 0.95em;
}
</style>