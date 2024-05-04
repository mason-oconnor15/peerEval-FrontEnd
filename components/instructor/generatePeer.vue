<template>
  <div>
    <h1>Peer Evaluation Report</h1>
    <label for="sectionId">Section ID:</label>
    <input type="text" id="sectionId" v-model="sectionId" required>
    <button @click="generateReport">Generate Report</button>
    <table v-if="reportEntries.length">
      <thead>
      <tr>
        <th>Student</th>
        <th>Grade</th>
        <th>Commented by</th>
        <th>Public comments</th>
        <th>Private comments</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="entry in reportEntries" :key="entry.id">
        <td>{{ entry.student }}</td>
        <td>{{ entry.grade }}</td>
        <td>{{ entry.commentedBy }}</td>
        <td>{{ entry.publicComments }}</td>
        <td>{{ entry.privateComments }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sectionId: '',
      reportEntries: [] // Fake data for the report
    };
  },
  methods: {
    generateReport() {
      // Generate report based on sectionId (not implemented, use fake data for now)
      this.reportEntries = Array.from({ length: 10 }, (_, index) => ({
        id: index + 1,
        student: `Student ${index + 1}`,
        grade: `${Math.floor(Math.random() * 60) + 40}/60`, // Random grade between 40 and 100
        commentedBy: `Teammate ${Math.floor(Math.random() * 10) + 1}`,
        publicComments: `Public comments for Student ${index + 1}`,
        privateComments: `Private comments for Student ${index + 1}`
      }));
    }
  }
};
</script>

