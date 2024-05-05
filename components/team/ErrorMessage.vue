<!-- ErrorMessage.vue -->
<template>
  <p class="error-message" v-if="message">{{ message }}</p>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
.error-message {
  color: red; /* Set the color of the error message */
  font-size: 14px; /* Set the font size */
  margin-top: 5px; /* Add some space between the input field and error message */
}
</style>
