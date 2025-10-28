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
    <div class="container">
      <div class="wrapper">
        <input
          id="name"
          type="text"
          required
          v-model="newContact.name"
          placeholder=" "
        />
        <label class="labelline" for="name">Name</label>
      </div>

      <div class="wrapper">
        <input
          id="phone"
          type="text"
          required
          v-model="newContact.number"
          placeholder=" "
        />
        <label class="labelline" for="phone">Phone</label>
      </div>
    </div>
    <button type="submit">Add</button>
  </form>
</template>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 16px;
  max-width: 350px;
  margin: 0 auto;
  padding: 24px;
  background: linear-gradient(
    var(--vt-c-indigo) 50%,
    var(--vt-c-divider-dark-2) 90%
  );
  box-shadow: 1px 5px 20px 1px rgba(0, 0, 0, 0.72);
  border: 1px solid var(--color-border, #333);
  border-radius: 12px;
  transition: all 0.3s ease;
}

.wrapper {
  position: relative;
  margin-top: 1.5rem;
}

input {
  width: 100%;
  padding: 12px 10px;
  font-size: 16px;
  background: none;
  border: 1px solid #555;
  border-radius: 8px;
  outline: none;
  color: #f0f0f0;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #42b883;
}

.labelline {
  position: absolute;
  left: 12px;
  top: 12px;
  color: #aaa;
  pointer-events: none;
  background-color: var(--vt-c-indigo);
  padding: 0 4px;
  transition: 0.3s ease all;
}

/* 🪄 Фокус або непорожній інпут */
input:focus + .labelline,
input:not(:placeholder-shown) + .labelline {
  top: -8px;
  left: 8px;
  font-size: 12px;
  color: #42b883;
}

input:focus {
  border-color: var(--vt-c-green, #42b883);
  box-shadow: 0 0 6px var(--vt-c-green, #42b883);
}

button {
  margin-top: 8px;
  padding: 10px 0;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  font-size: 15px;
  cursor: pointer;
  background: var(--vt-c-green, #42b883);
  color: white;
  transition:
    background 0.3s ease,
    transform 0.2s ease;
}

button:hover {
  background: #2d8f6e;
  transform: translateY(-1px);
}

button:active {
  transform: translateY(0);
}

@media (max-width: 480px) {
  .form {
    width: 100%;
    padding: 16px;
  }
}
</style>
