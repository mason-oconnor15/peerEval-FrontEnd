<template>
  <div class="container">
    <h2>Invite Instructors to Join a Senior Design Section</h2>
    <form @submit.prevent="inviteInstructor">
      <div class="entry">
        <label>Instructor emails: </label>
        <textarea v-model="emails" wrap="soft" @blur="checkEmail"></textarea>
      </div>
      <p v-if="badEmail" :style="{color: badEmailMessage.color}">{{ badEmailMessage.message }}</p>

      <div>
        <button :disabled="disableSubmit" type="submit">Invite</button>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    data(){ // data function
      return{
        emails: [],
        disableSubmit: true,
        badEmail: false,

        badEmailMessage: {
          message: '',
          color: '',
        }
      };
    },


    methods: { // method declarations
      checkEmail: function(){
        let rawEmailList = this.emails.split(',');
        let emailList = []
        for(const email in rawEmailList){
          emailList.push(rawEmailList[email].trim());
        }
        for(const email of emailList){
          if(!email.includes('@')){
            this.badEmail = true;
            this.badEmailMessage.message = 'One or more of the emails are not correctly formatted.';
            this.badEmailMessage.color = 'red'
            this.disableSubmit = true;
            return;
          }
        }

        this.emails = emailList;
        this.badEmail = false;
        this.badEmailMessage.message = '';
        this.badEmailMessage.color = '';
        this.disableSubmit = false;
      },


      inviteInstructor: function(){ // when the button is clicked
        console.log(this.emails);
        this.emails = '';
        alert("Email(s) has been sent.");
      },
    }
  }
</script>


<style scoped>
  div {
    font-size: 20px;
  }

  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  button {
    padding: 5px;
    width: 100%;
  }

  p {
    margin: 2px;
  }

  textarea {
    height: 150px;
    width: 400px;
    font-size: 15px;
  }
</style>