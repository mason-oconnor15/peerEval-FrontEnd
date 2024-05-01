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