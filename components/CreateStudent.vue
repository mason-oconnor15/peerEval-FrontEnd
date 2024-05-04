<template>
  <div class="container">
    <h2>Create A New Student Account</h2>
    <form @submit.prevent="submitStudent">
        <div class="labelAndInput">
            <label>First Name:</label>
            <input type="text" v-model="student.firstName"></input>
        </div>
        <div class="labelAndInput">
            <label>Middle Initial:</label>
            <input type="text" v-model="student.middleInitial"></input>
        </div>
        <div class="labelAndInput">
            <label>Last Name:</label>
            <input type="text" v-model="student.lastName"></input>
        </div>
        <div class="labelAndInput">
            <label>Password:</label>
            <input type="text" id="password" v-model="student.password"></input>
        </div>
        <p v-if="displayCheckPassword" :style="{ color: confirmPassword.messageColor }">{{ confirmPassword.message }}</p>
        <div class="labelAndInput">
            <label>Re-Enter Password:</label>
            <input type="text" id="checkPassword" v-model="confirmPassword.enteredPassword"  @blur="checkPasswords"></input>
        </div>
        <button :disabled="disableSubmit" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      // Data properties for your component
      student:{
        firstName: '',
        middleInitial: '',
        lastName: '',
        password: ''
      },
      confirmPassword:{
        enteredPassword: '',
        message: '',
        messageColor: 'black',
      },
      displayCheckPassword: false,
      disableSubmit: true,
    };
  },
  computed: {
    // Computed properties here
  },
  methods: {
    // Methods for your component
    submitStudent: /*async*/ function(){
        /*const formData = new FormData();
        formData.append("loan", JSON.stringify(loan));
        const response = await axios.post('localhost:8080/peereval/student', formData,);*/
        console.log("student submitted");
        //restore to default state
        this.student.firstName = '';
        this.student.lastName = '';
        this.student.middleInitial = '';
        this.student.password = '';
        this.confirmPassword.enteredPassword = '';
        this.confirmPassword.message = '';
        this.confirmPassword.messageColor ='black';
        this.displayCheckPassword = false;
    },
    checkPasswords() {
      this.displayCheckPassword = true;
      if (this.student.password === this.confirmPassword.enteredPassword) {
        this.confirmPassword.message = 'Passwords match!';
        this.confirmPassword.messageColor = 'green';
        this.disableSubmit = false;
      } else {
        this.confirmPassword.message = 'Passwords do not match!';
        this.confirmPassword.messageColor = 'red';
        this.disableSubmit = true;
      }

    }
  },
  watch: {
    // Watchers to respond to prop or data changes
  },
  // Lifecycle hooks
  created() {
    console.log('Component is created!');git
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
button{
  padding:5px;
}
p{
    margin: 2px;
}
</style>
