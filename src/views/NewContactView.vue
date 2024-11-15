<template>
  <div class="new-contact-container">
    <h2 class="title">New Contact</h2>
    <form @submit.prevent="addNewContact" class="contact-form">
      <input v-model.trim="firstName" placeholder="First Name" required class="input-field" />
      <input v-model.trim="lastName" placeholder="Last Name" required class="input-field" />
      <input v-model.trim="email" placeholder="Email" type="email" required class="input-field" />
      <button type="submit" class="submit-button">Add Contact</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useContactStore } from '../components/useContactStore'
import { useRouter } from 'vue-router'

export default {
  setup() {
    const contactStore = useContactStore()
    const router = useRouter()

    const firstName = ref('')
    const lastName = ref('')
    const email = ref('')

    const addNewContact = () => {
      const newContact = { 
        firstName: firstName.value, 
        lastName: lastName.value, 
        email: email.value 
      }
      const addedContact = contactStore.addContact(newContact)
      router.push(`/contact/${addedContact.id}`)

      // Reset form fields
      firstName.value = ''
      lastName.value = ''
      email.value = ''
    }

    return { firstName, lastName, email, addNewContact }
  }
}
</script>

<style scoped>
.new-contact-container {
  max-width: 400px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  color: #333;
  margin-bottom: 1.5rem;
  font-size: 1.5rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.input-field {
  padding: 0.75rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.input-field:focus {
  outline: none;
  border-color: #007bff;
}

.submit-button {
  padding: 0.75rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #0056b3;
}
</style>
  