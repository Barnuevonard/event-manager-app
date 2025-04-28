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
/* Ensure body takes up full height and remove overflow */
body, html {
  height: 100%;
  margin: 0;
  overflow: hidden; /* Prevent scroll */
}

.login {
  max-width: 400px;
  margin:  auto; /* Center horizontally */
  margin-top: 200px;
  padding: 20px;
  background-color: gray;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: auto; /* Let it adjust based on content */
  box-sizing: border-box; /* Include padding in element's total width and height */
  position: relative;
  top: 50%;
  transform: translateY(-50%); /* Center vertically */
}

input {
  display: block;
  width: 100%;
  padding: 0.8rem;
  margin: 0.5rem 0;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 0.8rem 1.2rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 1rem; /* Add some margin above the button */
}

button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  font-size: 0.9rem;
  margin-top: 1rem;
}
</style>

