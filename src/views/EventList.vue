<template>
  <div class="event-list">
    <h2>Upcoming Events</h2>
    <ul>
      <li v-for="(event, index) in events" :key="event.id">
        <div v-if="!event.isEditing">
          <h3>{{ event.name }}</h3>
          <p>{{ event.description }}</p>
          <p>{{ event.date }}</p>
          <button @click="startEditing(index)">Edit</button>
          <button @click="deleteEvent(index)">Delete</button>
        </div>

        <div v-else>
          <input v-model="events[index].name" />
          <textarea v-model="events[index].description"></textarea>
          <input v-model="events[index].date" type="date" />
          <button @click="saveEdit(index)">Save</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const events = ref([]);

const addEvent = (newEvent) => {
  events.value.push({
    ...newEvent,
    id: Date.now(), // Add unique ID
    isEditing: false
  });
};

const deleteEvent = (index) => {
  events.value.splice(index, 1); // Remove event at given index
};



defineExpose({
  addEvent,
});

const startEditing = (index) => {
  events.value[index].isEditing = true;
};

const saveEdit = (index) => {
  events.value[index].isEditing = false;
};


import { watch } from 'vue';

watch(events, (newEvents) => {
  localStorage.setItem('events', JSON.stringify(newEvents)); // Save to localStorage
}, { deep: true });

import { onMounted } from 'vue';

onMounted(() => {
  const savedEvents = localStorage.getItem('events');
  if (savedEvents) {
    events.value = JSON.parse(savedEvents); // Load events from localStorage
  }
});




</script>

<style scoped>
.event-list {
  max-width: 600px;
  margin: 2rem auto;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin: 1rem 0;
}
</style>
