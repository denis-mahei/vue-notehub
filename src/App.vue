<script setup lang="ts">
import { ref, onMounted, watch, type Ref } from 'vue'
import ContactForm from '@/components/ContactForm.vue'
import ContactList from '@/components/ContactList.vue'
import data from '@/data/data.json'
import type { Contact } from '@/types/contact.ts'

const contacts = ref<Contact[]>(data)

onMounted(() => {
  const savedContacts = localStorage.getItem('contacts')
  if (savedContacts) {
    contacts.value = JSON.parse(savedContacts)
  }
})

watch(
  contacts,
  (newContacts) => {
    localStorage.setItem('contacts', JSON.stringify(newContacts))
  },
  { deep: true },
)
const storeContact = (contact: Contact): void => {
  contacts.value.push(contact)
}

const deleteContact = (contactId: string) =>
  (contacts.value = contacts.value.filter(
    (contact) => contactId !== contact.id,
  ))
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
  <main>
    <section class="contact-form">
      <ContactForm @add-contact="storeContact" />
    </section>
    <section class="contacts">
      <ContactList :contacts="contacts" @delete-contact="deleteContact" />
    </section>
  </main>
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
main {
  padding: 20px;
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
.contacts {
  padding: 20px;
  margin-top: 16px;
}
</style>
