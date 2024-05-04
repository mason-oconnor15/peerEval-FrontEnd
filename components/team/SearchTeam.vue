<template>
  <!--
  In simpler terms, v-if="showSearchModule" controls whether the search
  container (and everything inside it) should be shown or hidden based
  on the value of showSearchModule. Because showSearchModule = true, that
  means we can see whats in the search-container
  -->
  <div class="search-container" v-if="showSearchModule">
    <h2>Search For Teams</h2>

    <!-- This for team name -->
    <p class="editInstructions">At least one search criterion must be specified.</p>
    <div class="inputContainer">
      <label>By Team Name: </label>
      <input v-model="searchCriteria.teamName">
    </div>

    <!-- This is for section name -->
    <div class="inputContainer">
      <label>By Section Name: </label>
      <input v-model="searchCriteria.sectionName">
    </div>

    <!-- This is for academic year -->
    <div class="defaultValueStyle">
      <label>By Academic Year: </label>

      <input v-model="searchCriteria.academicYear"
             :class="{ grayText: searchCriteria.academicYear === '2024' }"
             @input="checkAcademicYear">

      <!-- Defined my own tag with error message -->
      <error-message :message="academicYearErrorMessage" v-if="academicYearErrorMessage"></error-message>
    </div>

    <!-- This is for instructor -->
    <div class="inputContainer">
      <label>By Instructor: </label>
      <input v-model="searchCriteria.instructor">
    </div>

    <!-- Buttons to submit -->
    <button :disabled="disableSearch">Search</button> <!-- Bind to disableSearch -->
    <button :disabled="!enableBack" @click="goBack">Back</button>
  </div>

  <div class="searchResult-container" v-if="!showSearchModule">
    <h2>Search Results</h2>
    <table>
      <thead>
        <!-- These are the names of columns in the table -->
        <tr>
          <th>Team Name</th>
          <th>Team Members (Students)</th>
          <th>Instructors</th>
        </tr>
      </thead>

      <tbody>
      <tr v-for="team in foundTeams" :key="team.teamName">
        <!-- These things below are meant to populate the table -->
        <td>{{ team.teamName }}</td>

        <!-- Loops through the list of students in team and displays their name  -->
        <td>
          <ul>
            <li v-for="student in team.students" :key="student.id">{{ student.name }}</li>
          </ul>
        </td>

        <!-- Loops through the list of instructors in team and displays their name  -->
        <td>
          <ul>
            <li v-for="instructor in team.instructors" :key="instructor.id">{{ instructor.name }}</li>
          </ul>
        </td>
      </tr>
      </tbody>
    </table>

    <!-- This is just in case no teams were found, given the search criteria -->
    <div v-if="Object.keys(foundTeams).length === 0">
      <p>No matching teams found.</p>
    </div>
  </div>
</template>

<script>
import ErrorMessage from "~/components/team/ErrorMessage.vue";
import axios from 'axios'; //Import axios

export default {
  components: {
    ErrorMessage
  },

  data() {
    return {
      showSearchModule: true,

      enableBack: true,

      disableSearch: true,

      searchCriteria: {
        teamName: '',
        sectionName: '',
        academicYear: '2024',
        instructor: '',
      },

      foundTeams: {},

      pageable: {
        page: 0,
        size: 10,
        sort: 'academicYear desc, sectionName, teamName'
      },

      academicYearErrorMessage: '',
    };
  },

  methods: {
    clearErrorMessages() {
      this.academicYearErrorMessage = '';
    },

    goBack() {
      //Use window.history to navigate back
      window.history.back();
    },

    //Check if academic year is numeric, if it's not, output error message
    checkAcademicYear() {
      //Regular expression to match only numbers
      const numberRegex = /^[0-9]+$/;

      //Assuming `this.academicYear` holds the input value
      if(numberRegex.test(this.searchCriteria.academicYear)) {
        this.disableSearch = false; //Input contains only numbers
        this.academicYearErrorMessage = ''; //Clear any existing error message
      } else {
        this.disableSearch = true; //Input contains non-numeric characters
        this.academicYearErrorMessage = 'Please input only numbers.'; //Display error message
      }
    },

    search: async function () {
      const payload = {
        searchCriteria: this.searchCriteria, // Correct payload object
        pageable: this.pageable //Correct payload object
      };

      try {
        const response = await axios.get('http://localhost:8080/peerEval/teams/search', { params: payload }); // Use params for GET requests
        this.foundTeams = response.data; //Update foundSections with response data
      } catch (error) {
        console.error('Error searching teams:', error);
      }
    },
  },

  computed: {
  },

}
</script>

<style>
.search-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  align-self: center;
  font-size: 15px;
}

.defaultValueStyle {
}

.defaultValueStyle input.grayText {
  color: gray;
}

button {
  margin: 10px;
}

p {
  color: red;
  margin: 0;
}

.editInstructions {
  color: blue;
}
</style>