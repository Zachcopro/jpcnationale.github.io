<template>
    <div class="main d-flex">
        <div class="sideDetails">
            <Side1 />
        </div>
        <div class="detailsMain">
            <!-- <h1 class="text-center">Article details</h1> -->
            <div v-if="post">
                <Articles :post="post" :display="'d-none'" specialLike="specialLike" specialShare="specialShare" />
            </div>
            <div v-else class="min-vh-100 d-flex justify-content-center align-items-center">
                <div class="spinner-border text-pr imary" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
                <P class="d-block text-center"></P>
            </div>
            <div class="commentaires">
                <Commentaire />
            </div>
        </div>
    </div>
</template>

<script setup>
import Articles from '~/composants/Articles.vue';
import Commentaire from '~/composants/Commentaire.vue';
import Side1 from '~/composants/Side1.vue';
const user = ref('Région 4')
const route = useRoute()

const { data: post, error } = await useFetch(() => "https://jsonplaceholder.typicode.com/posts/" + route.params.id, {
    lazy: true,
    onError: (err) => {
        console.error("Erreur API:", err);
        throw createError({ statusCode: 404, message: "Article non trouvé" });
    }
});

useSeoMeta({
    title: () => post.value?.title
})
</script>

<style scoped>
.sideDetails {
    flex: 1;

}

.detailsMain {
    flex: 4;
    margin-top: 20px;
}

.userProfil {
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    margin-right: 1rem;
}

.div-text {
    margin-top: -1rem;
}

.bi-hand-thumbs-up {
    font-size: 1.2rem;
    left: 35%;
    top: 0;
}

.bi-reply {
    transform: scaleX(-1);
    font-size: 1.3rem;
    left: 35%;
    top: 0;

}

.actionPost {
    border-bottom: 1px solid rgb(197, 197, 197);
    margin-bottom: 5px;
}

@media (max-width: 815px) {
    .sideDetails {
        display: none !important;
    }

    .main {
        display: block;
        /* margin-top: 150px; */
    }

    .detailsMain {
        width: 100%;
        flex: none;
    }
}

@media screen and (max-width: 1270px) {
    .bi-hand-thumbs-up {
        font-size: 1.2rem;
        left: 25%;
        top: 0;
    }

    .bi-reply {
        transform: scaleX(-1);
        font-size: 1.3rem;
        left: 25%;
        top: 0;

    }
}

@media screen and (max-width: 620px) {
    .bi-hand-thumbs-up {
        font-size: 1.2rem;
        left: 5%;
        top: 0;
    }

    .bi-reply {
        transform: scaleX(-1);
        font-size: 1.3rem;
        left: 5%;
        top: 0;

    }
}
</style>