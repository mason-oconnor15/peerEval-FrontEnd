<template>
  <h2>Student Account Information</h2>

  <div class="get-id-container" v-if="this.needStudentId">
    <p>Enter your Student ID to proceed: </p>
    <input type="number" placeholder="Must be a number" v-model="this.studentId" @change="this.checkStudentId">
    <button :disabled="this.disableSubmitId" @click="this.sendStudentId">Submit</button>
  </div>


  <div class="account-container" v-else>
    <table>
      <thead>
        <th>First Name</th>
        <th>Last Name</th>
        <th></th>
        <th></th>
      </thead>

      <tbody>
        <tr>
          <td>
            <input type="text" v-model="this.returnedStudent.firstName" :disabled="this.disableFirstName" @change="this.enableSubmitChanges">
          </td>
          <td>
            <input type="text" v-model="this.returnedStudent.lastName" :disabled="this.disableLastName" @change="this.enableSubmitChanges">
          </td>
          <td>
            <button @click="this.enableEdit">Edit</button>
          </td>
          <td>
            <button :disabled="this.disableSubmitChanges" @click="this.sendChanges">Submit changes</button>
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
        needStudentId: true,
        studentId: '',
        disableSubmitId: true,

        returnedStudent: {},

        disableFirstName: true,
        disableLastName: true,
        disableSubmitChanges: true,
      }
    },


    methods: {
      checkStudentId: function() {
        if(this.studentId.length != 0){
          this.disableSubmitId = false;
        }
      },

      sendStudentId() {
        axios.get(this.baseUrl + "/student/" + this.studentId)
            .then(response => {
              this.returnedStudent = response.data.data;
            })
            .catch(error => {
              console.log(error);
            });

        this.needStudentId = false;
      },

      enableEdit: function() {
        this.disableFirstName = false;
        this.disableLastName = false;
      },

      enableSubmitChanges: function() {
        this.disableSubmitChanges = false;
      },

      sendChanges: function() {
        console.log(this.returnedStudent);
        axios.put(this.baseUrl + "/student/" + this.studentId, this.returnedStudent)
            .then(response => {
              console.log(this.returnedStudent);
              console.log(response);
            })
            .catch(error => {
              console.log(error);
            })
      }
    },
  }
</script>

<style scoped>
  .get-id-container, h2, .account-container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-self: center;
    font-size: 20px;
    margin: 10px;
  }
</style>