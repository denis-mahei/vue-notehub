<script setup lang="ts">
import ContactItem from '@/components/ContactItem.vue'
defineProps(['contacts'])
const emit = defineEmits(['delete-contact'])
</script>

<template>
  <ul class="list-item">
    <ContactItem
      v-for="contact in contacts"
      :key="contact.id"
      :name="contact.name"
      :number="contact.number"
      :id="contact.id"
      @delete-contact="emit('delete-contact',contact.id)"
    />
  </ul>
</template>

<style scoped>
.list-item {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
</style>
