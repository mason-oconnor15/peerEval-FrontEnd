<template>
  <div>
    <h1>Set Up an Instructor Account</h1>
    <form @submit.prevent="submitForm">
      <label for="firstName">First Name:</label>
      <input type="text" id="firstName" v-model="formData.firstName" required><br>

      <label for="middleInitial">Middle Initial:</label>
      <input type="text" id="middleInitial" v-model="formData.middleInitial" maxlength="1"><br>

      <label for="lastName">Last Name:</label>
      <input type="text" id="lastName" v-model="formData.lastName" required><br>

      <label for="password">Password:</label>
      <input type="password" id="password" v-model="formData.password" required><br>

      <label for="confirmPassword">Confirm Password:</label>
      <input type="password" id="confirmPassword" v-model="confirmPassword" required><br>

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  data() {
    return {
      formData: {
        firstName: '',
        middleInitial: '',
        lastName: '',
        password: ''
      },
      confirmPassword: ''
    };
  },
  methods: {
    submitForm() {
      if (this.formData.password !== this.confirmPassword) {
        alert('Passwords do not match');
        return;
      }

      // Implement form submission logic here
      console.log('Form submitted:', this.formData);
    }
  }
};
</script>

<style scoped>
/* Add your CSS styles here */
label {
  display: inline-block;
  width: 150px;
  margin-bottom: 5px;
}
input {
  width: 200px;
  margin-bottom: 10px;
}
button {
  margin-top: 10px;
}
</style>
