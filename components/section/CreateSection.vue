<template>
    <div class="container">
      <h2>Create A New Section</h2>
  
      <form @submit.prevent="submitNewSection">

        <div class="labelAndInput">
          <label>Section Name:</label>
          <input type="text" v-model="section.sectionName" @input="checkSectionName"></input>
          <error-message :message="section.sectionNameErrorMessage" />
        </div>

        <div class="labelAndInput">
          <label>Academic Year:</label>
          <input type="text" v-model="section.academicYear" @input="checkAcademicYear"></input>
          <error-message :message="section.academicYearErrorMessage" />
        </div>

        <div class="labelAndInput">
          <label>First & Last Date of the Academic Year:</label>
          <input type="text" v-model="section.firstAndLastDate" @input="checkFirstAndLastDate"></input>
          <error-message :message="section.firstAndLastDateErrorMessage" />
        </div>
  
        <button :disabled="disableSubmit" type="submit">Submit</button>
        <button :disabled="!enableBack" @click="goBack">Back</button>
        <p v-if="showWarning" class="warning-message">
            Warning: Any unsaved changes will be lost if you navigate back.
        </p>

      </form>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  import ErrorMessage from '../section/ErrorMessage.vue'
  
  export default {
    components: {
        ErrorMessage
    },
    data() {
      return {
        enableBack: true,
        showWarning: false, //warnin message is initally not visible
        initialSectionName: '',
        initialAcademicYear: '',
        initialFirstAndLastDate: '',

        section: {
          sectionName: '',
          academicYear: '',
          firstAndLastDate: ''
        },
  
        disableSubmit: true,
        sectionNameErrorMessage: '',
        academicYearErrorMessage: '',
        firstAndLastDateErrorMessage: ''
      };
    },
  
    computed: {
      //Computed properties here
    },

    mounted() {
      console.log('Component is mounted on the DOM.');
      // Store initial values of text fields when the component is mounted
      this.initialSectionName = this.section.sectionName;
      this.initialAcademicYear = this.section.academicYear;
      this.initialFirstAndLastDate = this.section.firstAndLastDate;
    },
  
    methods: {
        goBack() {
            if (confirm("Are you sure you want to navigate back? Any unsaved changes will be lost.")) {
                // Use window.history to navigate back
                window.history.back();
            } else {
                // Restore initial values of text fields
                this.section.sectionName = this.initialSectionName;
                this.section.academicYear = this.initialAcademicYear;
                this.section.firstAndLastDate = this.firstAndLastDate;
                
            }
        },

        submitNewSection: function() {
            console.log("New section has been created.");
    
            //Restore to default state
            this.section.sectionName = '';
            this.section.academicYear = '';
            this.section.firstAndLastDate = '';
            this.section.disableSubmit = true;
            this.clearErrorMessages();
        },
    
        checkSectionName() {
            if(this.section.sectionName != null) {
            this.disableSubmit = false;
            this.section.sectionNameErrorMessage = '';
            } else {
            this.disableSubmit = true;
            this.section.sectionNameErrorMessage = 'Please input a section name.'
            }
        },

        checkAcademicYear() {
            // Regular expression to match only numbers
            const numberRegex = /^[0-9]+$/;

            // Assuming `this.section.academicYear` holds the input value
            if (numberRegex.test(this.section.academicYear)) {
                this.disableSubmit = false; // Input contains only numbers
                this.section.academicYearErrorMessage = ''; // Clear any existing error message
            } else {
                this.disableSubmit = true; // Input contains non-numeric characters
                this.section.academicYearErrorMessage = 'Please input only numbers.'; // Display error message
            }
        },

        checkFirstAndLastDate() {
            // Assuming this.startDate and this.endDate hold the input values
            const dateRegex = /^\d{2}\/\d{2}\/\d{4}\s*-\s*\d{2}\/\d{2}\/\d{4}$/;
            if (dateRegex.test(this.section.firstAndLastDate)) {
                this.disableSubmit = false; // Dates are formatted correctly
                this.section.firstAndLastDateErrorMessage = ''; // Clear any existing error message
            } else {
                this.disableSubmit = true; // Dates are not formatted correctly
                this.section.firstAndLastDateErrorMessage = 'Please input dates in the format MM/DD/YYYY - MM/DD/YYYY.';
            }
        },

        clearErrorMessages() {
        this.sectionNameErrorMessage = '';
        this.academicYearErrorMessage = '';
        this.firstAndLastDateErrorMessage = '';
        }

    },
  
    watch: {
      //Watchers to respond to prop or data changes
    },
  
    //Lifecycle hooks
    created() {
      console.log('Component is created!');
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
    padding:5px;
  }
  
  p {
    margin: 2px;
  }
  
  .warning-message {
  color: red;
  font-style: italic;
  }

  </style>