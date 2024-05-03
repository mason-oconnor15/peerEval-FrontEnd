<script setup>
    
</script>
<template>
    <div class="container">
        <NuxtLink :to="{ path: '/student/create' }">
            <button>create student</button>
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
      <NuxtLink :to="{ path: '/team/create' }">
        <button>create team</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/section/create/createSectionsPage' }">
        <button>Create Section</button>
      </NuxtLink>
      <NuxtLink :to="{ path: '/section/search/searchSectionsPage' }">
        <button>Find a Section</button>
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