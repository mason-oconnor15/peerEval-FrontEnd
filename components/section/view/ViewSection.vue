<template>
    <div class="container">
      <table>
        <thead>
            <th>Section Name</th>
            <th>Acadmeic Year</th>
            <th>Team Info</th>
            <th>Instructors</th>
            <th>Students</th>
        </thead>
        <tbody>
            <tr :v-model="this.section.sectionName"></tr>
            <tr :v-model="this.section.academicYear"></tr>
            <tr :v-model="this.section.teamInfo"></tr>
            <tr :v-model="this.section.instructors"></tr>
            <tr :v-model="this.section.students"></tr>
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
            section:{},
        };
    },
    computed: {
      // Computed properties here
    },
    methods: {
      // Methods for your component
      fetchSection: async function(){
        axios.get("localhost:8080/section/");
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