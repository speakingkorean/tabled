<template>
  <div class="container">
    <div class="top-bar">
      <div class="date">{{ formattedDate }}</div>
      <div>
        <button @click="openModal" class="add-button">Add</button>
        <button @click="openList" class="add-button">List</button>
      </div>
    </div>
    <!-- {{ reservations }} -->
    <div class="body-content">
      <div v-if="isModalVisible" class="modal-overlay">
        <div class="modal">
          <h2>Add Reservation</h2>
          <form @submit.prevent="handleFormSubmit">
            <label for="time">When:</label>
            <input type="time" id="time" v-model="reservation.time">
            <br>
            <label for="size">How many people:</label>
            <input type="number" id="size" v-model="reservation.size" min="1" max="35">
            <br>
            <label for="name">Name:</label>
            <input type="text" id="name" v-model="reservation.name" />
            <br>
            <label for="contact">Contact Number:</label>
            <input type="text" id="contact" v-model="reservation.contact" />
            <br>
            <label for="duration">How long:</label>
            <input type="number" id="duration" v-model="reservation.duration" min="30" max="180">
            <div class="modal-actions">
              <button type="button" @click="closeModal">Close</button>
              <button type="submit">Submit</button>
            </div>
          </form>
        </div>
      </div>
      <div v-if="isListVisible" class="modal-overlay">
        <div class="modal">
          <h2>List</h2>
          {{ reservations }}
          <div class="modal-actions">
            <button type="button" @click="closeList">Close</button>
          </div>
        </div>
      </div>
      <div class="grid-container">
        <div class="grid-cell grid-span-2">Table 1</div>
        <div class="grid-cell">Table 4A</div>
        <div class="grid-cell">Table 4</div>
        <div class="grid-cell grid-span-2">Table 2</div>
        <div class="grid-cell">Table 5A</div>
        <div class="grid-cell">Table 5</div>
        <div class="grid-cell grid-span-2">Table 3</div>
        <div class="grid-cell">Table 6A</div>
        <div class="grid-cell">Table 6</div>
        <div class="empty-cell grid-span-3"></div>
        <div class="grid-cell">Table 7</div>
        <div class="empty-cell grid-span-3"></div>
        <div class="grid-cell">Table 8</div>
        <div class="empty-cell grid-span-3"></div>
        <div class="grid-cell">Table 9</div>
        <div class="empty-cell grid-span-3"></div>
        <div class="grid-cell">Table 10</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'
const today = ref(new Date())
const reservations = ref([])
const reservationDefault = {
  time: '18:30',
  size: 2,
  name: '',
  contact: '',
  duration: 90,
}
const reservation = reactive({ ...reservationDefault })
const isModalVisible = ref(false)
const isListVisible = ref(false)

const openModal = () => {
  isModalVisible.value = true
}

const closeModal = () => {
  isModalVisible.value = false
}

const openList = () => {
  isListVisible.value = true
}

const closeList = () => {
  isListVisible.value = false
}

const handleFormSubmit = () => {
  console.log('you clicked submit')
  reservations.value.push(reservation)
  // todo: need to RESET
  // reservation.value = { ...reservationDefault }
  closeModal()
}

const showList = () => {
  console.log('you clicked showList')
}

const formattedDate = computed(() => {
  const options = {
    weekday: 'long', // Full day name (e.g., "Friday")
    month: 'long',   // Full month name (e.g., "April")
    day: 'numeric',  // Day of the month (e.g., 4)
  }
  return today.value.toLocaleDateString('en-US', options)
})
</script>

<style scoped>
/* The main container will use flex to stack the child divs vertically */
.container {
  display: flex;
  flex-direction: column;
  /* Stack children vertically */
  height: 100vh;
  /* Full viewport height */
  padding: 20px;
}

/* Sticky top bar */
.top-bar {
  position: sticky;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #333;
  color: white;
  padding: 20px;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

/* Add padding to the content below the top-bar to prevent it from being hidden */
.body-content {
  padding-top: 80px;
  /* Adjust according to your top bar height */
  flex: 1;
}

.date {
  font-size: 18px;
  margin-bottom: 10px;
}

.add-button {
  padding: 8px 16px;
  font-size: 16px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin: 2px 40px;
}

.add-button:hover {
  background-color: #45a049;
}

/* Modal overlay styling */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

/* Modal styling */
.modal {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.modal-actions {
  display: flex;
  justify-content: space-between;
}

.modal-actions button {
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}

/* Define the grid container */
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  /* Create 3 equal-width columns */
  gap: 10px;
  /* Space between cells */
  padding: 10px;
}

.grid-cell {
  background-color: #4caf50;
  color: white;
  text-align: center;
  font-size: 18px;
  padding: 20px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.grid-cell:hover {
  background-color: #45a049;
}

.empty-cell {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.grid-span-2 {
  grid-column: span 2;
}

.grid-span-3 {
  grid-column: span 3;
}
</style>