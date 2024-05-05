<template>
  <div>
    <h1>WAR Report</h1>
    <button @click="generateReport">Generate Report</button>
    <table v-if="reportEntries.length">
      <thead>
      <tr>
        <th>Student</th>
        <th>Task Category</th>
        <th>Planned Task</th>
        <th>Description</th>
        <th>Planned Hours</th>
        <th>Actual Hours</th>
        <th>Status</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="entry in reportEntries" :key="entry.id">
        <td>{{ entry.student }}</td>
        <td>{{ entry.taskCategory }}</td>
        <td>{{ entry.plannedTask }}</td>
        <td>{{ entry.description }}</td>
        <td>{{ entry.plannedHours }}</td>
        <td>{{ entry.actualHours }}</td>
        <td>{{ entry.status }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      reportEntries: [] // Fake data for the report
    };
  },
  methods: {
    generateReport() {
      this.reportEntries = Array.from({ length: 10 }, (_, index) => ({
        id: index + 1,
        student: `Student ${index + 1}`,
        taskCategory: `Task Category ${Math.floor(Math.random() * 3) + 1}`,
        plannedTask: `Planned Task ${Math.floor(Math.random() * 5) + 1}`,
        description: `Description ${index + 1}`,
        plannedHours: Math.floor(Math.random() * 10) + 1,
        actualHours: Math.floor(Math.random() * 10) + 1,
        status: Math.random() < 0.5 ? 'Done' : 'In Progress'
      }));
    }
  }
};
</script>

