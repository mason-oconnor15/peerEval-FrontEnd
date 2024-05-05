<script setup>
    
import War from "~/pages/instructor/war.vue";
</script>
<template>
    <div class="container">
        <NuxtLink :to="{ path: '/student/create' }">
            <button>create student</button>
        </NuxtLink>
      <NuxtLink :to="{ path: '/student/peereval/submitpeereveal' }">
        <button>Submit Peer Evaluation Form</button>
      </NuxtLink>
        <NuxtLink :to="{ path: '/student/search' }">
            <button>find student</button>
        </NuxtLink>
      <NuxtLink :to="{ path: '/section/activeweeks' }">
        <button>set active weeks</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/instructor/instracc' }">
        <button>Setup Instructor account</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/instructor/war' }">
        <button>Generate War</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/instructor/peer' }">
        <button>Instructor -Generate Peer Evaluation</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/student/peereval/viewpe' }">
        <button>Student-View Peer Eval</button>
      </NuxtLink>

      <!-- Ana's stuff -->
      <NuxtLink :to="{ path: '/team/searchTeam' }">
        <button>Search Team</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/team/createTeam' }">
        <button>Create Team</button>
      </NuxtLink>


      <NuxtLink :to="{ path: '/section/create/createSectionsPage' }">
        <button>Create Section</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/section/search/searchSectionsPage' }">
        <button>Find a Section</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/rubric/create/createRubricPage' }">
        <button>Create a Rubric</button>
      </NuxtLink>


      <NuxtLink :to="{ path: '/instructor/invite' }">
        <button>Invite instructors</button>
      </NuxtLink>

      <NuxtLink :to="{ path: '/instructor/search' }">
        <button>Search For Instructors</button>
      </NuxtLink>
    </div>
</template>
<style>
    .container{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    button{
        padding:10px;
        font-size: 15px;
    }
</style>