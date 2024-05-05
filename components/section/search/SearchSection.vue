<template>
    <div class="search-container" v-if="showSearchModule"> <!-- Correct syntax for v-if -->
        <h2>Search For A Section</h2>
        <div class="inputContainer">
            <label>By Section Name:</label>
            <input v-model="searchCriteria.sectionName">
        </div>
        <div class="inputContainer">
            <label>By Academic Year:</label>
            <input v-model="searchCriteria.academicYear" @input="checkAcademicYear">
            <error-message :message="academicYearErrorMessage" v-if="academicYearErrorMessage"></error-message> <!-- Display error message if academicYearErrorMessage exists -->
        </div>
        

        <button :disabled="disableSearch" @click="search">Search</button> <!-- Bind to disableSearch -->
        <button :disabled="!enableBack" @click="goBack">Back</button>

    </div>
    <div class="searchResult-container" v-if="!showSearchModule"> <!-- Correct syntax for v-if -->
        <table>
            <thead>

            </thead>
            <tbody v-for="section in foundSections"></tbody>
        </table>
    </div>
</template>

<script>
import ErrorMessage from '../ErrorMessage.vue'
import axios from 'axios'; // Import axios

export default {
    components: {
        ErrorMessage
    },
    data() {
        return {
            enableBack: true,
            showSearchModule: true,
            disableSearch: true,
            searchCriteria: {
                sectionName: '',
                academicYear: ''
            },
            foundSections: {},
            pageable: {
                page: 0,
                size: 10,
                sort: 'academicYear, asc'
            },
            academicYearErrorMessage: '',
        };
    },
    methods: {
        goBack() {
            // Use window.history to navigate back
            window.history.back();
        },

        checkAcademicYear() {
            // Regular expression to match only numbers
            const numberRegex = /^[0-9]+$/;

            // Assuming `this.academicYear` holds the input value
            if (numberRegex.test(this.searchCriteria.academicYear)) {
                this.disableSearch = false; // Input contains only numbers
                this.academicYearErrorMessage = ''; // Clear any existing error message
            } else {
                this.disableSearch = true; // Input contains non-numeric characters
                this.academicYearErrorMessage = 'Please input only numbers.'; // Display error message
            }
        },

        search: async function () {
            const payload = {
                searchCriteria: this.searchCriteria, // Correct payload object
                pageable: this.pageable // Correct payload object
            };
            try {
                const response = await axios.get('http://localhost:8080/peerEval/section/search', { params: payload }); // Use params for GET requests
                this.foundSections = response.data; // Update foundSections with response data
            } catch (error) {
                console.error('Error searching sections:', error);
            }
        },

        clearErrorMessages() {
            this.academicYearErrorMessage = '';
        }
    },
    computed: {

    }
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

button {
    margin: 10px;
}

p {
    color: red;
    margin: 0;
}
</style>