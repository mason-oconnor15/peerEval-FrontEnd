<template>
  <div class="container">
    <h2>Information of Instructor</h2>
    <table>
      <thead>
        <th>Name</th>
        <th>Teams</th>
        <th>Status</th>
      </thead>

      <tbody>
        <tr>
          <td>{{this.instructor.name}}</td>
          <td>{{this.instructor.teamName}}</td>
          <td>{{this.instructor.status}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import axios from "axios";
  export default {
    data(){
      return{
        instructor: {
          instructorId: '',
          name: '',
          academicYear: '',
          teamName: '',
          status: '',
        },
        //
        // nothing: this.fetchInstructorData(),

        fetchDataCall: this.fetchInstructorData(),
      };
    },


    methods: {
      getInstructorId: function (){
        const urlParam = new URLSearchParams(window.location.search);
        const instructorId = urlParam.get('instructorId');
        return instructorId;
      },

      fetchInstructorData(){
        const instructorId = this.getInstructorId();
        axios.get("http://localhost:8080/peereval/instructors/"+instructorId)
            .then(response => {
              // console.log(response.data.data);
              // return response.data.data;
              this.instructor = response.data.data;
            })
            .catch(error => {
              console.log(error);
            });
      }
    }
  }
</script>

<style scoped>
  .container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-self: center;
    font-size: 20px;
  }

  table{
    text-align: center;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid black;
    padding: 10px;
  }
</style>