<template>
    <div class="comments">
        <!-- Formulaire de nouveau commentaire -->
        <div class="newComment mx-auto bg-white">
            <img class="userProfil" src="/userProfil.jpg" alt="Photo de profil">
            <input type="text" class="newText form-control bg-light" placeholder="Nouveau commentaire...">
            <i class="bi bi-send fs-2 btn bg-light rounded-circle mx-3"></i>
        </div>

        <!-- Liste des commentaires -->
        <div class="listComments mx-auto mt-4 bg-white">
            <!-- Affichage des commentaires visibles -->
            <Comment v-for="(commentaire, index) in visibleComments" :key="commentaire.id" :commentaire="commentaire" />

            <!-- Bouton de contrôle -->
            <div class="text-center mt-3" v-if="commentaires.length > 2">
                <button @click="toggleComments" class="btn btn-link p-0 text-decoration-none">
                    {{ showAll ? 'Voir moins' : `Voir tout (${commentaires.length})` }}
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Comment from './Comment.vue';

const showAll = ref(false);

const commentaires = ref([
    {
        id: 1,
        autheur: 'Zach',
        text: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Pariatur ex aliquid earum!'
    },
    {
        id: 2,
        autheur: 'Lionel',
        text: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Pariatur ex aliquid earum!'
    },
    {
        id: 3,
        autheur: 'Russel',
        text: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Pariatur ex aliquid earum!'
    },
    {
        id: 4,
        autheur: 'David',
        text: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Pariatur ex aliquid earum!'
    }
]);

// Calcul des commentaires visibles
const visibleComments = computed(() => {
    return showAll.value ? commentaires.value : commentaires.value.slice(0, 2);
});

function toggleComments() {
    showAll.value = !showAll.value;
}
</script>

<style scoped>
.userProfil {
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    margin-right: 1rem;
}

.newComment {
    width: 98%;
    border-radius: 7px;
    display: flex;
    padding: 30px 5px;
    align-items: center;
}

.listComments {
    width: 98%;
    border-radius: 7px;
    padding: 20px 5px;
}

.newText {
    border-radius: 20px;
    flex-grow: 1;
    padding: 10px 15px;
}

.bi-send {
    transform: rotate(45deg);
    transition: transform 0.2s ease;
}

.bi-send:hover {
    transform: rotate(45deg) scale(1.1);
}

/* Animation pour les commentaires */
/* Ajoutez cette règle */
.listComments {
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>