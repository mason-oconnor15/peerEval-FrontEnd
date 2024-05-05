<template>
    <div class="container">
      <table>
        <thead>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Acadmeic Year</th>
            <th>Team</th>
            <th>Peer Evaluations</th>
            <th>WARs</th>
            <th>Delete Student</th>
        </thead>
        <tbody>
            <tr>
              <td>{{ this.student.firstName }}</td>
              <td>{{ this.student.lastName }}</td>
              <td>{{ this.student.academicYear }}</td>
              <td>{{ this.student.teamName || "No Team"}}</td>
              <td>{{ this.student.numberOfPeerEvals || 0 }}</td>
              <td>{{ this.student.numberOfWars }}</td>
              <td> <button @click="deleteStudent(student.id)">Delete</button> </td>
            </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  export default {
    data() {
      return {
            // Data properties for your component
            student:{},
        };
    },
    computed: {
      // Computed properties here
    },
    methods: {
      // Methods for your component
      fetchStudent: async function(studentId){
        try{
          const response = await axios.get(`http://localhost:8080/peerEval/student/${studentId}`);
          this.student= response.data.data;
          console.log(response.data);
          console.log(this.student);
        }
        catch(error){
          alert("Error fetching student: " + error);
        }
      },
      deleteStudent: function(studentId){
        try{
          const response = axios.delete(`localhost:8080/student/${studentId}`);
        }
        catch(error){
          alert("Error deleting student: " + error);
        }
      }
    },
    watch: {
      // Watchers to respond to prop or data changes
    },
    // Lifecycle hooks
    created() {
      console.log('Component is created!');
    },
    mounted() {
      const studentId= this.$route.params.studentId;
      this.fetchStudent(studentId);
      console.log('Component is mounted on the DOM.');
    },
    // You can add more lifecycle hooks here like updated, destroyed, etc.
  }
  </script>
  
  <style scoped>
  /* Scoped CSS styles for this component */
  div {
    font-size: 20px;
  }
  .container{
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
  }
  p{
      margin: 2px;
  }
  table {
    border-collapse: collapse; /* This ensures that adjacent cells share borders */
    
  }
  td, th {
    border: 1px solid black; /* Add a solid black border to all table cells */
    justify-items: center;
    align-items: center;
  }
  </style>