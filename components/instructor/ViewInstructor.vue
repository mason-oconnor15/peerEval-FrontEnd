<template>
  <div class="container">
    <h2>Information of Instructor</h2>
    <table>
      <thead>
        <th>Name</th>
        <th>Teams</th>
        <th>Status</th>
        <th></th>
      </thead>

      <tbody>
        <tr>
          <td>{{this.instructor.name}}</td>
          <td>{{this.instructor.teamName}}</td>
          <td>{{this.instructor.status}}</td>
          <td>
            <NuxtLink v-if="this.instructor.status == 'IS_DEACTIVATED'" :to="{path:'/instructor/view/changestatus', query:{id: this.instructor.instructorId, action : 'reactivate'}}">
              <button>Reactivate this Instructor</button>
            </NuxtLink>

            <NuxtLink v-if="this.instructor.status == 'IS_ACTIVE'" :to="{path:'/instructor/view/changestatus', query:{id: this.instructor.instructorId, action : 'deactivate'}}">
              <button>Deactivate this Instructor</button>
            </NuxtLink>
          </td>
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
        baseUrl: "http://localhost:8080/peerEval",
        instructor: {
          instructorId: '',
          name: '',
          academicYear: '',
          teamName: '',
          status: '',
        },

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
        axios.get("http://localhost:8080/peerEval/instructors/" + instructorId)
            .then(response => {
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