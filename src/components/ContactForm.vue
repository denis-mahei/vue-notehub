<script setup lang="ts">
import { reactive } from 'vue'

const emit = defineEmits(['add-contact'])

const newContact = reactive({
  name: '',
  number: '',
})

const handleSubmit = () => {
  emit('add-contact', { ...newContact, id: Date.now().toString() })
  newContact.name = ''
  newContact.number = ''
}
</script>

<template>
  <form @submit.prevent="handleSubmit" class="form">
    <label for="name">Name</label>
    <input id="name" type="text" required v-model="newContact.name" />

    <label for="phone">Phone</label>
    <input id="phone" type="text" required v-model="newContact.number" />

    <button type="submit">Add</button>
  </form>
</template>

<style scoped>
  .form {
    display: flex;
    max-width: 300px;
    flex-direction: column;
    border: 1px solid var(--color-border);
    background-color: #2c3e50;
  }
</style>
