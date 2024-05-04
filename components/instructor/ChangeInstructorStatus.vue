<template>
  <div class="deactivate-container" v-if="this.showDeactivate">
    <h2>Deactivate an Instructor</h2>
    <p>Enter reason for deactivation:</p>
    <textarea v-model="this.deactivateBody.reason" @blur="this.checkReason"></textarea>

    <p>Confirm that you want to deactivate this instructor?</p>
    <button :disabled="this.disableConfirm" @click="this.sendDeactivateRequest">Confirm</button>
    <button @click="this.goBack()">Cancel</button>
  </div>

  <div class="reactivate-container" v-else>
    <h2>Reactivate an Instructor</h2>
    <p>Confirm that you want to reactivate this instructor?</p>
    <button @click="this.sendReactivateRequest">Confirm</button>
    <button @click="this.goBack()">Cancel</button>
  </div>
</template>

<script>
  import axios from "axios";
  export default {
    data(){
      return {
        showDeactivate: this.showDeactivateStatus(),
        instructorId: this.fetchInstructorId(),
        deactivateBody: {
          reason: '',
        },
        disableConfirm: true,

        deactivatedInstructor: {

        }
      }
    },


    methods: {
      fetchAction: function(){
        const urlParam = new URLSearchParams(window.location.search);
        const action = urlParam.get("action");
        return action;
      },

      fetchInstructorId: function(){
        const urlParam = new URLSearchParams(window.location.search);
        const instructorId = urlParam.get("id");
        return instructorId;
      },

      showDeactivateStatus: function() {
        const action = this.fetchAction();
        if(action == 'deactivate'){
          return true;
        }else{
          return false;
        }
      },

      sendDeactivateRequest: async function(){
        axios.put("http://localhost:8080/peereval/instructors/deactivate/" + this.instructorId, this.deactivateBody)
            .then((response) => {
              console.log(response);
              alert(response.data.message);
              this.$router.push('../search');
            })
            .catch(error => {
              console.log(error);
            });
      },

      goBack: function(){
        this.$router.back();
      },

      checkReason: function(){
        if(this.deactivateBody.reason.length != 0){
          this.disableConfirm = false;
        }
      },

      sendReactivateRequest: async function(){
        axios.put("http://localhost:8080/peereval/instructors/reactivate/" + this.instructorId)
            .then((response) => {
              alert(response.data.message);
              console.log(response);
              this.$router.push('../search');
            })
            .catch(error => {
              console.log(error);
            })
      }
    }
  }
</script>

<style scoped>
  .deactivate-container, .reactivate-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-self: center;
    font-size: 20px;
  }
</style>