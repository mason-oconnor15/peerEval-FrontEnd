<template>
  <button @click="removeStudent">Remove This Student</button>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    teamName: String,
    studentId: Number,
  },

  methods: {
    async removeStudent() {
      try {
        const teamName = this.$props.teamName;
        const studentId = this.$props.studentId;

        await axios.put(`http://localhost:8080/peerEval/teams/${teamName}/remove/students/${studentId}`);
        //Backend updates the data and returns a success message
        console.log('Student removed successfully');

        //Event to notify the parent component the student was removed
        this.$emit('student-removed');
      } catch (error) {
        console.error('Error removing student:', error);
      }
    },

  },

};
</script>
