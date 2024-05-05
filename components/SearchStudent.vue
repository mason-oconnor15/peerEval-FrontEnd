<template>
    <div class="search-container" v-if="this.showSearchModule">
        <h2>Search For A Student</h2>
        <div class="inputContainer">
            <label>First Name:</label>
            <input v-model="searchCriteria.firstName">
        </div>
        <div class="inputContainer">
            <label>Last Name:</label>
            <input v-model="searchCriteria.lastName">
        </div>
        <div class="inputContainer">
            <label>Section:</label>
            <input v-model="this.searchCriteria.sectionName">
        </div>
        <p v-if="this.yearCheck.showMsg">{{ this.yearCheck.invalInputMsg }}</p>
        <div class="inputContainer">
            <label>Academic Year:</label>
            <input v-model="this.searchCriteria.academicYear" @blur="checkYear">
        </div>
        <div class="inputContainer">
            <label>Team Name:</label>
            <input v-model="this.searchCriteria.teamName">
        </div>
        <button :disabled="this.disableSearch" @click="search">Search</button>
    </div>
    <div class="searchResult-container" v-if="!this.showSearchModule">
        <table>
            <thead>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Section Name</th>
                <th>Academic Year</th>
                <th>Team Name</th>
                <th>View</th>
            </thead>
            <tbody>
                    <tr v-for="student in this.foundStudents" :key="student.id">
                        <td>{{ student.firstName }}</td>
                        <td>{{ student.lastName }}</td>
                        <td>{{ student.sectionName || "No Data" }} </td>
                        <td>{{ student.academicYear || "No Data" }} </td>
                        <td>{{ student.teamName || "No Data" }}</td>
                        <NuxtLink :to="{ path: `/student/view/${student.id}` }">
                            <button>View This Student</button>
                        </NuxtLink>
                    </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
import axios from "axios";
export default{
    data(){
        return{
            showSearchModule: true,
            disableSearch: false,
            searchCriteria:{
                firstName: '',
                lastName:'',
                sectionName:'',
                academicYear:'',
                teamName:''
            },
            yearCheck:{
                invalInputMsg: 'Year must only contain numbers',
                showMsg: false,
            },
            foundStudents:{},
            pageable: {
                page: 0,
                size: 10,
                sort: 'academicYear, desc'
            }
        };
    },
    methods:{
        validateYear: function(){
            let input = this.searchCriteria.academicYear;
            let isnum = /^\d+$/.test(input);
            if (isnum){
                this.disableSearch = false;
                this.yearCheck.showMsg = false;
            }
            else if(this.searchCriteria.academicYear === ""){
                this.disableSearch = false;
                this.yearCheck.showMsg = false;
            } 
            else{
                this.yearCheck.showMsg = true;
            }
        },
        checkYear: function(){
            this.disableSearch = true;
            this.validateYear();
        },
        search: async function(){
            axios.post("http://localhost:8080/peerEval/student/search", this.searchCriteria, this.paging)
            .then((response) => {
              console.log(response.data.data.content);
              this.foundStudents = response.data.data.content;
              this.showSearchModule = false;
            })
            .catch(error => {
              console.log(error);
            })
        }
    },
    computed:{

    }
}
</script>
<style>
    .search-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        align-self: center;
        font-size: 15px;
    }
    .searchResult-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        align-self: center;
        font-size: 15px;
    }
    td{
        border-width: 5px;
        color: black;
    }
    th{
        border-width: 5px;
        color: black;
    }
    button{
        margin:10px;
    }
    p{
        color: red;
        margin:0;
    }

</style>