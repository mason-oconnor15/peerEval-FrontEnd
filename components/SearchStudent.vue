<template>
    <div class="search-container" :v-if="this.showSearchModule">
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
            <input v-model="this.searchCriteria.academicYear" @blur="validateYear">
        </div>
        <div class="inputContainer">
            <label>Team Name:</label>
            <input v-model="this.searchCriteria.teamName">
        </div>
        <button :disabled="this.disableSearch">Search</button>
    </div>
    <div class="searchResult-container" :v-if="!this.showSearchModule">
        <table>
            <thead>

            </thead>
            <tbody v-for="student in this.foundStudents"></tbody>
        </table>
    </div>
</template>
<script>
export default{
    data(){
        return{
            showSearchModule: true,
            disableSearch: true,
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
                sort: 'academicYear, asc'
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
            else{
                this.yearCheck.showMsg = true;
            }
        },
        search: async function(){
            const payload = {
                searchCriteria,
                pageable
            };
            const response = await axios.get('http://localhost:8080/peerEval/student/search', payload)
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
    button{
        margin:10px;
    }
    p{
        color: red;
        margin:0;
    }

</style>