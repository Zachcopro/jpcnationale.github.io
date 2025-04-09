<template>
    <div v-if="post" class="card mb-3">
        <div class="card-body">
            <div class="d-flex align-items-center">
                <img class="userProfil" src="/userProfil.jpg" alt="Photo de profil">
                <div class="d-flex flex-column ms-2">
                    <p class="mb-0 fw-semibold">{{ user }}</p>
                    <div class="d-flex align-items-center text-muted">
                        <small class="text-body-secondary">3 min</small>
                        <span class="mx-1">·</span>
                        <i class="bi bi-globe-europe-africa fs-6"></i>
                    </div>
                </div>
            </div>

            <h5 class="card-title mt-2 mb-4">{{ post.title }}</h5>
            <TextTruncated :text="post.body" :truncate-lines="2" :char-limit="70" button-label-expanded="Réduire"
                button-label-collapsed="Lire plus" gradient-color="rgba(255,255,255,0.9)" />

            <img src="/img1.jpg" class="card-img-top mt-2 rounded" alt="Image de l'article">

            <div class="d-flex justify-content-between align-items-center text-muted mt-2">
                <div>
                    <i class="bi bi-hand-thumbs-up-fill text-white bg-primary rounded-circle p-1 me-1"></i>
                    <span v-if="likesCount > 0" class="small">{{ likesCount }}</span>
                </div>
                <div class="small">
                    <span>48 commentaires · </span>
                    <span>6 partages · </span>
                    <span>372 vues</span>
                </div>
            </div>

            <hr class="my-2">

            <div class="d-flex justify-content-around">
                <button @click="toggleLike" class="btn btn-like" :class="{ 'text-primary': isLiked }">
                    <i class="bi me-1" :class="isLiked ? 'bi-hand-thumbs-up-fill' : 'bi-hand-thumbs-up'"></i>
                    J'aime
                </button>
                <NuxtLink :to="`/articles/${post.id}`" class="btn">
                    <i class="bi bi-chat me-1"></i>
                    Commenter
                </NuxtLink>
                <button class="btn">
                    <i class="bi bi-share me-1"></i>
                    Partager
                </button>
            </div>
        </div>
    </div>

    <div v-else class="min-vh-100 d-flex justify-content-center align-items-center">
        <div class="spinner-border text-primary" role="status">
            <span class="visually-hidden">Chargement...</span>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import TextTruncated from './TextTruncated.vue';

const props = defineProps({
    post: {
        type: Object,
        required: true
    }
});

const user = ref('Région 4');
const isLiked = ref(false);
const likesCount = ref(12); // Valeur initiale des likes

// Fonction toggle pour le like
const toggleLike = () => {
    if (isLiked.value) {
        likesCount.value--;
    } else {
        likesCount.value++;
    }
    isLiked.value = !isLiked.value;

    // Ici vous pourriez ajouter un appel API pour sauvegarder le like
    // await $fetch('/api/likes', { method: 'POST', body: { postId: props.post.id } })
};
</script>

<style scoped>
.userProfil {
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    object-fit: cover;
}

.card-img-top {
    max-height: 400px;
    object-fit: cover;
}

.btn-like {
    transition: color 0.2s ease;
}

.btn-like:hover {
    color: var(--bs-primary) !important;
}

.btn {
    font-size: 0.9rem;
    padding: 0.5rem 0;
}

.btn i {
    font-size: 1.1rem;
}

/* Responsive */
@media (max-width: 576px) {
    .btn span {
        display: none;
    }

    .btn i {
        font-size: 1.3rem;
        margin-right: 0 !important;
    }
}
</style>