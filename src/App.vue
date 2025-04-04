<!-- 
 publish github page
 fix top bar for scroll
 modal for adding reservation
 list of reservations
-->
<template>
  <div class="container">
    <div class="top-bar">
      <div class="date">{{ formattedDate }}</div>
      <button @click="handleAddClick" class="add-button">Add</button>
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
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    // Reactive state (replacing 'data')
    const today = ref(new Date());

    // Computed property (replacing 'computed')
    const formattedDate = computed(() => {
      const options = {
        weekday: 'long', // Full day name (e.g., "Friday")
        month: 'long',   // Full month name (e.g., "April")
        day: 'numeric',  // Day of the month (e.g., 4)
      };
      return today.value.toLocaleDateString('en-US', options);
    });

    // Method (replacing 'methods')
    const handleAddClick = () => {
      alert('Add button clicked!');
    };

    // Return values to the template
    return {
      today,
      formattedDate,
      handleAddClick,
    };
  },
};
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

/* Top bar styling (first div), center-aligning items */
.top-bar {
  background-color: #333;
  color: white;
  padding: 20px;
  margin-bottom: 20px;
  /* Add space below the top bar */
  display: flex;
  flex-direction: column;
  /* Stack the date and button vertically */
  align-items: center;
  /* Center align items horizontally */
  justify-content: center;
  /* Center items vertically */
}

.date {
  font-size: 18px;
  margin-bottom: 10px;
  /* Add space between the date and the button */
}

.add-button {
  padding: 8px 16px;
  font-size: 16px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-button:hover {
  background-color: #45a049;
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