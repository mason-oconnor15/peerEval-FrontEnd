<template>
  <div>
    <h1>Peer Evaluation Report</h1>
    <button @click="generateReport">Generate Report</button>
    <div v-if="report">
      <h2>{{ report.student }}</h2>
      <table>
        <thead>
        <tr>
          <th>Criteria</th>
          <th>Score</th>
          <th>Comments</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(criteria, score) in report.scores" :key="criteria">
          <td>{{ criteria }}</td>
          <td>{{ score }}</td>
          <td>{{ report.comments[criteria] }}</td>
        </tr>
        </tbody>
      </table>
      <p>Overall Grade: {{ report.overallGrade }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      report: null
    };
  },
  methods: {
    generateReport() {
      // Generate random data for the report
      const criteria = ['Quality of Work', 'Teamwork', 'Communication', 'Initiative'];
      const scores = {};
      const comments = {};
      let totalScore = 0;

      criteria.forEach(criterion => {
        const score = Math.floor(Math.random() * 10) + 1; // Random score between 1 and 10
        scores[criterion] = score;
        comments[criterion] = `Comments for ${criterion}`;
        totalScore += score;
      });

      const overallGrade = `${totalScore}/${criteria.length * 10}`; // Calculate overall grade

      this.report = {
        student: 'John Doe', // Fake student name
        scores: scores,
        comments: comments,
        overallGrade: overallGrade
      };
    }
  }
};
</script>
