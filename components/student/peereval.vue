<template>
  <div class="peer-evaluation-form">
    <h1>Peer Evaluation Form</h1>
    <div v-for="(teamMember, index) in teamMembers" :key="index" class="team-member">
      <h2>{{ teamMember.name }}</h2>
      <label>Quality of Work (1-10):</label>
      <input v-model="teamMember.qualityOfWork" type="number" min="1" max="10">
      <!-- Add other evaluation criteria as needed -->
    </div>
    <button @click="submitEvaluation" class="submit-button">Submit Evaluation</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'PeerEvaluationForm',
  setup() {
    const teamMembers = ref([
      { name: 'John Doe', qualityOfWork: null },
      { name: 'Lily Fisher', qualityOfWork: null },
      { name: 'Tim Smith', qualityOfWork: null },
      // Add other team members here
    ]);

    const submitEvaluation = () => {
      const evaluations = teamMembers.value.map((member) => ({
        name: member.name,
        qualityOfWork: member.qualityOfWork,
        // Add other evaluation criteria as needed
      }));

      // Assuming you have an API service to send the evaluations
      // apiService.submitEvaluations(evaluations);

      // Reset the form after submission
      teamMembers.value.forEach((member) => {
        member.qualityOfWork = null;
        // Reset other evaluation criteria as needed
      });
    };

    return {
      teamMembers,
      submitEvaluation,
    };
  },
};
</script>

<style scoped>
.peer-evaluation-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.team-member {
  margin-bottom: 20px;
}

.submit-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #0056b3;
}
</style>
