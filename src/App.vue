<script setup lang="ts">
import { ref, computed, watch } from 'vue'
import ContactForm from '@/components/ContactForm.vue'
import ContactList from '@/components/ContactList.vue'
const contacts = ref([
  { id: 'id-1', name: 'Rosie Simpson', number: '459-12-56' },
  { id: 'id-2', name: 'Hermione Kline', number: '443-89-12' },
  { id: 'id-3', name: 'Eden Clements', number: '645-17-79' },
  { id: 'id-4', name: 'Annie Copeland', number: '227-91-26' },
])

const storeContact = (contact) => {
  contacts.value.push(contact)
}
const deleteContact = (contactId) =>
 contacts.value = contacts.value.filter((contact) => contactId !== contact.id)
</script>

<template>
  <!-- start Header -->
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="60" />

    <div class="wrapper">
      <h1>ContactBook</h1>
      <p>Save your contact's</p>
    </div>

    <a href="https://ua.vuejs.org/">
      <img src="@/assets/logo.svg" alt="logo" class="logo" width="60" />
    </a>
  </header>
  <ContactForm @add-contact="storeContact" />
  <ContactList :contacts="contacts" @delete-contact="deleteContact"/>
</template>

<style scoped>
header {
  line-height: 1.5;
  display: flex;
  justify-content: space-between;
  padding: 20px;
  width: 100%;
  align-items: center;
  background-image: linear-gradient(var(--vt-c-indigo), var(--vt-c-black-mute));
}
.wrapper {
  padding: 16px;
  border-radius: 10px;
  background: linear-gradient(
    var(--color-background),
    var(--vt-c-divider-dark-2)
  );
  box-shadow: 1px 5px 20px 1px rgba(0, 0, 0, 0.72);
}

h1,
p {
  text-align: center;
}
.logo {
  display: block;
}
/* ми пояснимо, що ці класи роблять далі! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
