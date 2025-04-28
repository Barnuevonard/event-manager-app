<template>
  <div class="create-event">
    <h2>Create Event</h2>
    <form @submit.prevent="createEvent">
      <input v-model="event.name" placeholder="Event Name" required />
      <input v-model="event.date" type="date" required />
      <textarea v-model="event.description" placeholder="Event Description" required></textarea>
      <button type="submit">Create Event</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const event = ref({
  name: '',
  date: '',
  description: '',
});

const emit = defineEmits(['eventCreated']);

function createEvent() {
  // Send the new event to the parent component
  emit('eventCreated', { ...event.value });
  // Clear the form after submission
  event.value.name = '';
  event.value.date = '';
  event.value.description = '';
}
</script>

<style scoped>
.create-event {
  max-width: 400px;
  margin: 2rem auto;
}
input,
textarea {
  width: 100%;
  margin: 1rem 0;
  padding: 0.5rem;
}
button {
  padding: 0.5rem 1rem;
  background-color: #007bff;
  color: white;
  border: none;
}
</style>
