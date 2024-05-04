<template>
  <div class="container">
    <h2>Create A New Team</h2>

    <form @submit.prevent="submitNewTeam">

    <!--
    * Only have 1 field because this is the only detail that needs to be defined
    * The 'associated information' only says team name should be defined
    -->
      <div class="labelAndInput">
        <label>Team Name:</label>
        <input type="text" v-model="team.teamName" @blur="checkTeamName"></input>
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
      team: {
        teamName: ''
      },

      disableSubmit: true
    };
  },

  computed: {
    //Computed properties here
  },

  /*
  * I should have a method that checks if there is already a team with the given name
  */
  methods: {
    submitNewTeam: function() {
      console.log("New team submitted (created).");

      //Restore to default state
      this.team.teamName = '';
    },

    checkTeamName() {
      if(this.team.teamName != null) {
        this.disableSubmit = false;
      } else {
        this.disableSubmit = true;
      }
    }
  },

  watch: {
    //Watchers to respond to prop or data changes
  },

  //Lifecycle hooks
  created() {
    console.log('Component is created!');
  },
  
  mounted() {
    console.log('Component is mounted on the DOM.');
  },
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
  padding:5px;
}

p {
  margin: 2px;
}
</style>