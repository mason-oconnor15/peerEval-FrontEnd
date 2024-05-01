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
        </thead>
        <tbody>
            <tr :v-model="this.student.firstName"></tr>
            <tr :v-model="this.student.lastName"></tr>
            <tr :v-model="this.student.academicYear"></tr>
            <tr :v-model="this.student.teamName"></tr>
            <tr :v-model="this.student.peerEvals"></tr>
            <tr :v-model="this.student.wars"></tr>
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
      fetchStudent: async function(){
        axios.get("localhost:8080/student/");
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
  </style>