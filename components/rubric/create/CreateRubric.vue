<template>
    <div class="container">
      <h2>Create A New Rubric</h2>
  
      <form @submit.prevent="submitNewRubric">
  
        <div class="labelAndInput">
          <label>Rubric Name:</label>
          <input type="text" v-model="rubric.rubricName" @input="checkRubricName"></input>
          <error-message :message="rubric.rubricNameErrorMessage" />
        </div>
  
        <div class="labelAndInput">
          <label>Rubric Criteria:</label>
          <!-- Add Criteria Button -->
          <button @click="addCriteria">Add Criteria</button>
        </div>
  
        <!-- Table for Rubric Criteria -->
        <table>
          <thead>
            <tr>
              <th>Criteria Name</th>
              <th>Criteria Description</th>
              <th>Criteria Max Score</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(criteria, index) in rubric.rubricCriteria" :key="index">
              <td><input type="text" v-model="criteria.name" @input="checkFilledRows"></td>
              <td><input type="text" v-model="criteria.description" @input="checkFilledRows"></td>
              <td><input type="number" v-model.number="criteria.maxScore" @input="checkFilledRows"></td>
            </tr>
          </tbody>
        </table>
  
        <error-message :message="rubricCriteriaErrorMessage" />

        <button :disabled="disableSubmit || !isTableFilled" type="submit">Submit</button>
        <button :disabled="!enableBack" @click="goBack">Back</button>
        <p v-if="showWarning" class="warning-message">
          Warning: Any unsaved changes will be lost if you navigate back.
        </p>
  
      </form>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  import ErrorMessage from '../ErrorMessage.vue'
  
  export default {
    components: {
      ErrorMessage
    },
    data() {
    return {
        enableBack: true,
        showWarning: false,
        initialRubricName: '',
        rubric: {
        rubricName: '',
        rubricCriteria: [
            { name: '', description: '', maxScore: null }
        ]
        },
        disableSubmit: true,
        rubricNameErrorMessage: '',
        rubricCriteriaErrorMessage: null, // Initialize with null or an empty message
        newCriteria: { name: '', description: '', maxScore: null },
        isTableFilled: false,
        criteriaComplete: true
    };
    },
  
    mounted() {
      console.log('Component is mounted on the DOM.');
      this.initialRubricName = this.rubric.rubricName;
    },
  
    methods: {
      goBack() {
        if (confirm("Are you sure you want to navigate back? Any unsaved changes will be lost.")) {
          window.history.back();
        } else {
          this.rubric.rubricName = this.initialRubricName;
        }
      },
  
      submitNewRubric() {
        // Check if all rubric criteria are filled
        this.criteriaComplete = this.rubric.rubricCriteria.every(criteria => 
            criteria.name.trim() !== '' && criteria.description.trim() !== '' && criteria.maxScore !== null
        );
        
        if (!this.criteriaComplete) {
            // Display error message if any criterion is incomplete
            return;
        }
        console.log("New rubric has been created.");
        this.rubric.rubricName = '';
        this.disableSubmit = true;
        this.clearErrorMessages();
      },
  
      checkRubricName() {
        if (this.rubric.rubricName !== null && this.rubric.rubricName.trim() !== '') {
          this.disableSubmit = false;
          this.rubricNameErrorMessage = '';
        } else {
          this.disableSubmit = true;
          this.rubricNameErrorMessage = 'Please input a rubric name.';
        }
      },
  
      clearErrorMessages() {
        this.rubricNameErrorMessage = '';
        this.rubricCriteriaErrorMessage = '';
      },
  
      addCriteria() {
        // Add new criteria to the list
        this.rubric.rubricCriteria.push({ ...this.newCriteria });
        // Clear new criteria object for next addition
        this.newCriteria = { name: '', description: '', maxScore: null };
      },
  
      checkFilledRows() {
        // Check if there's at least one filled row in the table
        for (const criteria of this.rubric.rubricCriteria) {
            if (criteria.name.trim() !== '' || criteria.description.trim() !== '' || criteria.maxScore !== null) {
            this.isTableFilled = true;
            this.rubricCriteriaErrorMessage = null;
            return;
            }
        }
        // If no filled row is found, disable submit button
        this.isTableFilled = false;
        this.rubricCriteriaErrorMessage = "There must be at least one criteria. Criteria must be completely filled."
        }
    },
  
    created() {
      console.log('Component is created!');
    }
  }
  </script>
  
  <style scoped>
  /* Styles remain the same */
  </style>
  