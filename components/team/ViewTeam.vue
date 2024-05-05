<template>
  <div class="container">
    <table>
      <thead>
      <tr>
        <th>Team Name</th>
        <th>Team Members (Students)</th>
        <th>Instructors</th>
        <th>Delete Team</th>
      </tr>
      </thead>

      <tbody>
      <tr>
        <td>
          <table>
            <tr>
              <th>Team Name</th>
              <th>Update Team</th>
            </tr>
            <tr>
              <td>{{ team.teamName }}</td>
              <td><button>Update This Team</button></td>
            </tr>
          </table>
        </td>

        <!-- Display students in a table cell -->
        <td>
          <table>
            <tr>
              <th>Student Name</th>
              <th>Remove Student</th>
            </tr>

            <tr v-for="student in team.students" :key="student.id">
              <td>{{ student.name }}</td>
              <td>
                <!-- Include RemoveStudent component for each student -->
                <remove-student
                    :teamName="team.teamName"
                    :studentId="student.id"
                    @student-removed="handleStudentRemoved"
                ></remove-student>
              </td>
            </tr>

          </table>
        </td>

        <!-- Display instructors in a table cell -->
        <td>
          <table>
            <tr>
              <th>Instructor Name</th>
              <th>Remove Instructor</th>
            </tr>
            <tr v-for="instructor in team.instructors" :key="instructor.id">
              <td>{{ instructor.name }}</td>
              <td>
                <!-- Include RemoveInstructor component for each instructor -->
                <remove-instructor
                    :teamName="team.teamName"
                    :instructorId="instructor.id"
                    @instructor-removed="handleInstructorRemoved"
                ></remove-instructor>
              </td>
            </tr>
          </table>
        </td>

        <!-- The button to delete team -->
        <td>
          <button>Delete This Team</button>
        </td>
      </tr>
      </tbody>

    </table>
  </div>
</template>

<script>
import axios from "axios";
import RemoveStudent from "./RemoveStudent.vue";
import RemoveInstructor from "./RemoveInstructor.vue";

export default {
  components: {
    RemoveStudent,
    RemoveInstructor,
  },

  data() {
    return {
      team: {
        teamName: '',
        students: [],
        instructors: [],
      },
    };
  },

  created() {
    this.getTeamDetails();
  },

  methods: {
    getTeamName() {
      const urlParams = new URLSearchParams(window.location.search);
      return urlParams.get('teamName');
    },

    async getTeamDetails() {
      const teamName = this.getTeamName();

      try {
        const response = await axios.get('http://localhost:8080/peerEval/teams/' + teamName);
        this.team = response.data;
      } catch (error) {
        console.error('Error fetching team details:', error);
      }
    },

  },
};
</script>

<style>
table {
  margin: 0 auto; /* Center the table horizontally */
  text-align: center;
  border-collapse: collapse;
  width: 80%; /* Adjust the width of the table as needed */
}

th, td {
  border: 1px solid black;
  padding: 10px;
}
</style>