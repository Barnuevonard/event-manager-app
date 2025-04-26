<template>
  <div class="login">
    <h2>Login</h2>
    <form @submit.prevent="handleLogin">
      <input v-model="username" placeholder="Username" />
      <input v-model="password" type="password" placeholder="Password" />
      <button type="submit">Login</button>
    </form>
    <p v-if="error" class="error">Invalid credentials</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Reactive properties for form inputs and error handling
const username = ref('')
const password = ref('')
const error = ref(false)

// Hardcoded valid user credentials
const validUser = {
  username: 'admin',
  password: '1234'
}

// Define the emit function to send data to parent component
const emit = defineEmits(['login'])

// Handle form submission and login logic
function handleLogin() {
  if (username.value === validUser.username && password.value === validUser.password) {
    // If credentials are correct, emit login event to parent
    emit('login', validUser.username)
  } else {
    // If credentials are incorrect, show error message
    error.value = true
  }
}
</script>

<style scoped>
.login {
  max-width: 300px;
  margin: 2rem auto;
}
input {
  display: block;
  width: 100%;
  margin: 0.5rem 0;
}
.error {
  color: red;
}
</style>
