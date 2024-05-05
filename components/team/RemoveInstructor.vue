<template>
  <button @click="removeInstructor">Remove This Instructor</button>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    teamName: String,
    instructorId: String,
  },

  methods: {
    async removeInstructor() {
      try {
        const teamName = this.$props.teamName;
        const instructorId = this.$props.instructorId;

        await axios.put(`http://localhost:8080/peerEval/teams/${teamName}/remove/instructors/${instructorId}`);
        //Backend updates the data and returns a success message
        console.log('Instructor removed successfully');
      } catch (error) {
        console.error('Error removing instructor:', error);
      }
    },
  },

};
</script>
