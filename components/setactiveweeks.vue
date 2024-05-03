<template>
  <div>
    <h1>Set Active Weeks for Sections</h1>
    <div class="calendar">
      <div v-for="(week, index) in weeks" :key="index" class="week" @click="toggleWeek(index)">
        Week {{ index + 1 }}
        <span v-if="activeWeeks.includes(index)">Active</span>
      </div>
    </div>
    <button @click="confirmSetup">Confirm Setup</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const weeks = Array.from({ length: 12 }, (_, index) => index + 1);
    const activeWeeks = ref([]);

    const toggleWeek = (week) => {
      if (activeWeeks.value.includes(week)) {
        activeWeeks.value = activeWeeks.value.filter(w => w !== week);
      } else {
        activeWeeks.value = [...activeWeeks.value, week];
      }
    };

    const confirmSetup = () => {
      console.log("Active Weeks:", activeWeeks.value);
      // Send active weeks to backend for storage
      // Implement this functionality as per your backend requirements
    };

    return { weeks, activeWeeks, toggleWeek, confirmSetup };
  }
};
</script>

<style scoped>
/* Add your CSS styles here */
.calendar {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
.week {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: center;
  cursor: pointer;
}
.week:hover {
  background-color: #f0f0f0;
}
.week span {
  margin-left: 5px;
  font-weight: bold;
  color: green;
}
</style>
