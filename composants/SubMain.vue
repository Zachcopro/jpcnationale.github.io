<template>

    <ActuPopulaire class="mb-4" />

    <div class="d-flex gap-5">
        <div class="Articles">
            <!-- <ListArticles /> -->
            <div v-if="posts">
                <Articles v-for="(post, index) in posts" :key="index" :post="post" />
            </div>
            <div v-else class="min-vh-100 d-flex justify-content-center align-items-center">
                <div class="spinner-border text-pr imary" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
                <P class="d-block text-center"></P>
            </div>
        </div>
        <div class="side2">
            <Side2 />
        </div>
    </div>
</template>

<script setup>
import ActuPopulaire from './ActuPopulaire.vue';
import Articles from './Articles.vue';
import Side2 from './Side2.vue';
const jaime = ref(null)

const AddJaime = () => {
    jaime.value++
}
const { data: posts } = await useFetch('https://jsonplaceholder.typicode.com/posts?_limit=19', {
    lazy: true
})
</script>

<style>
.Articles {
    flex: 2;
}

.side2 {
    flex: 1;
}

/* responsive */
@media (max-width: 750px) {
    .side2 {
        display: none !important;
    }
}
</style>