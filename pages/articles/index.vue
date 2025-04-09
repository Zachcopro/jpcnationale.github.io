<template>
    <Main />
</template>

<script setup>
import Main from '~/composants/Main.vue';
const { data: posts } = await useFetch('https://jsonplaceholder.typicode.com/posts?_limit=20', {
    lazy: true
})  
</script>