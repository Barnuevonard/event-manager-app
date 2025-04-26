<template>
  <div>
    <h1>Event Manager App</h1>
    <div v-if="!user">
      <LoginPage @login="loginUser" /> <!-- Listen for the login event -->
    </div>
    <div v-else>
      <p>Welcome, {{ user }}!</p>
      <button @click="logoutUser">Logout</button>
      <!-- Event management UI will go here next -->
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LoginPage from './views/LoginPage.vue';  

// State to track logged in user
const user = ref(null)

// Function to handle login event
function loginUser(username) {
  user.value = username;  // Set the logged-in username
}

// Function to handle logout
function logoutUser() {
  user.value = null;  // Reset the user to null when logging out
}
</script>

<style scoped>
h1 {
  text-align: center;
  margin-top: 2rem;
}
</style>
