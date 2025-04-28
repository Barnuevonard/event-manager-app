<template>
  <div >
    <div>
      <h1>Event Manager App</h1>
    </div>
    
    <div v-if="!user">
      <LoginPage @login="loginUser" /> <!-- Listen for the login event -->
    </div>
    <div v-else>
      <p>Welcome, {{ user }}!</p>
      <button @click="logoutUser">Logout</button>
      <!-- Event management UI will go here next -->
      <CreateEvent @eventCreated="addEvent" />
      <EventList ref="eventList" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LoginPage from './views/LoginPage.vue';
import CreateEvent from './views/CreateEvent.vue';
import EventList from './views/EventList.vue';  

// State to track logged in user
const user = ref(null)

const eventList = ref(null);

// Function to handle login event
function loginUser(username) {
  user.value = username;  // Set the logged-in username
}

// Function to handle logout
function logoutUser() {
  user.value = null;  // Reset the user to null when logging out
}

// Function to add event to event list (when event is created)
function addEvent(event) {
  if (eventList.value) {
    eventList.value.addEvent(event);
  }
}



</script>

<style scoped>
h1 {
  text-align: center;
  margin-top: 2rem;
 
}





</style>
