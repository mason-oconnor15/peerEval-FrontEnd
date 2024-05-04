<template>
  <div class="search-container" v-if="this.showSearchOptions" @change="checkCriteria">
    <h2>Search For Instructors</h2>
    <p>At least one search criterion must be specified.</p>
    <div class="search-entry">
      <label>Name: </label>
      <input v-model="searchCriteria.name" type="text" placeholder="Name contains..."/>
    </div>


    <div class="search-entry">
      <label>Academic year: </label>
      <input v-model="searchCriteria.academicYear" type="number"/>
    </div>


    <div class="search-entry">
      <label>Status </label>
      <input v-model="searchCriteria.status" type="radio" name="status" value="IS_ACTIVE" />Active
      <input v-model="searchCriteria.status" type="radio" name="status" value="IS_DEACTIVATED" />Deactivated
      <input v-model="searchCriteria.status" type="radio" name="status" value="" />Any
    </div>


    <button :disabled="this.badCriteria" @click="searchWithCriteria">Search</button>
  </div>

  <div class="result-container" v-if="this.showResults">
    <h2>Search Results</h2>
    <table>
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">Academic Year</th>
          <th scope="col">Teams</th>
          <th scope="col">Status</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="instructor in this.searchResults" :key="instructor.instructorId">
          <td>{{instructor.name}}</td>
          <td>{{instructor.academicYear}}</td>
          <td>{{instructor.teamNames}}</td>
          <td>{{instructor.status}}</td>
          <td>
            <NuxtLink :to="{ path: '/instructor/view/[instructorId]', query: { instructorId: instructor.instructorId } }">
              <button>View This Instructor</button>
            </NuxtLink>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data(){
      return {
        showSearchOptions: true,
        badCriteria: false,

        searchCriteria:{
          name: '',
          academicYear: '',
          status: '',
        },

        paging:{
          page: 0,
          size: 1,
          sort: 'name,asc',
        },

        showResults: false,
        searchResults: {},
      }
    },


    methods: {
      checkCriteria: function (){
        if(this.searchCriteria.name.length != 0
        || this.searchCriteria.academicYear.length != 0){
          this.badCriteria = false;
        }
      },

      searchWithCriteria: function(){
        axios.post("http://localhost:8080/peereval/instructors/search", this.searchCriteria, this.paging)
            .then((response) => {
              console.log(response.data.data.content);
              this.searchResults = response.data.data.content;
            })
            .catch(error => {
              console.log(error);
            })
        this.showSearchOptions = false;
        this.showResults = true;
      }
    }
  }
</script>

<style scoped>
  .search-container, .result-container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-self: center;
    font-size: 20px;
  }

  .search-entry{
    margin: 5px;
  }

  button{
    margin: 10px;
  }

  p{
    color: red;
    margin: 5px;
  }

  table{
    text-align: center;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid black;
    padding: 10px;
  }
</style>