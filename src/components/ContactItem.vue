<script setup lang="ts">
import { Icon } from '@iconify/vue'
defineProps({
  id: String,
  name: String,
  number: String,
})
const emit = defineEmits(['delete-contact'])
</script>

<template>
  <li class="wrapper">
    <div class="item">
      <p>{{ name }}</p>
      <p>{{ number }}</p>
    </div>
    <button class="btn" @click="emit('delete-contact', id)">
      <Icon icon="line-md:trash" width="24" height="24" />
    </button>
  </li>
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: space-between;
  width: 300px;
}
.btn {
  background: transparent;
  border: none;
  color: #ff0000;
}
.item {
}
</style>
