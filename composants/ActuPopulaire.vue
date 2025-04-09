<template>
    <div class="card d-block border-0 shadow-sm">
        <div id="adaptiveCarousel" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-indicators">
                <button v-for="(_, index) in slideGroups" :key="index" type="button" data-bs-target="#adaptiveCarousel"
                    :data-bs-slide-to="index" :class="{ active: index === 0 }"
                    :aria-label="'Slide ' + (index + 1)"></button>
            </div>

            <div class="carousel-inner rounded-top">
                <div v-for="(group, groupIndex) in slideGroups" :key="groupIndex" class="carousel-item"
                    :class="{ active: groupIndex === 0 }" data-bs-interval="10000">
                    <div class="d-flex">
                        <div v-for="(slide, slideIndex) in group" :key="slideIndex" class="slide-item"
                            :style="{ width: itemWidth }">
                            <img :src="slide.img" class="img img-fluid w-100" :style="{
                                'height': itemsPerSlide === 1 ? '350px' : '280px',
                                'object-fit': 'cover',
                                'object-position': 'center'
                            }" :alt="'Content ' + (groupIndex * itemsPerSlide + slideIndex + 1)">
                        </div>
                    </div>
                </div>
            </div>

            <button class="carousel-control-prev" type="button" data-bs-target="#adaptiveCarousel" data-bs-slide="prev">
                <span class="carousel-control-prev-icon bg-dark rounded-circle p-3" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#adaptiveCarousel" data-bs-slide="next">
                <span class="carousel-control-next-icon bg-dark rounded-circle p-3" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div>

        <div class="card-body d-flex flex-wrap justify-content-between align-items-center gap-3 p-3">
            <!-- Groupe de boutons d'actions -->
            <div class="d-flex gap-2">
                <!-- Bouton Like -->
                <button class="btn btn-action position-relative" @click="toggleLike">
                    <i class="bi bi-hand-thumbs-up-fill action-icon" :class="{ 'text-primary': isLiked }"></i>
                    <span class="action-text">Aimer</span>
                    <span v-if="likeCount > 0"
                        class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                        {{ likeCount }}
                    </span>
                </button>

                <!-- Bouton Follow -->
                <button class="btn btn-action" @click="toggleFollow">
                    <i class="bi bi-wifi action-icon" :class="{ 'text-success': isFollowing }"></i>
                    <span class="action-text">Suivre</span>
                </button>

                <!-- Bouton Share -->
                <button class="btn btn-action" @click="shareContent">
                    <i class="bi bi-share-fill action-icon"></i>
                    <span class="action-text">Partager</span>
                </button>

                <!-- Menu déroulant -->
                <div class="dropdown">
                    <button class="btn btn-action" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="bi bi-three-dots"></i>
                    </button>
                    <ul class="dropdown-menu dropdown-menu-end shadow-sm">
                        <li><a class="dropdown-item" href="#"><i class="bi bi-bookmark me-2"></i>Enregistrer</a></li>
                        <li><a class="dropdown-item" href="#"><i class="bi bi-flag me-2"></i>Signaler</a></li>
                    </ul>
                </div>
            </div>

            <!-- Groupe de boutons secondaires -->
            <div class="d-flex gap-2">
                <button class="btn btn-primary px-3 rounded-pill fw-medium">
                    Learn More
                </button>
                <button class="btn btn-outline-secondary px-3 rounded-pill">
                    <i class="bi bi-chat-dots-fill me-1"></i>
                    <span>Message</span>
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';

const slides = ref([
    { img: '/jpc1.jpg' },
    { img: '/jpc2.jpg' },
    { img: '/jpc3.jpg' },
    { img: '/jpc1.jpg' },
    { img: '/jpc2.jpg' },
    { img: '/jpc3.jpg' }
]);

const windowWidth = ref(process.client ? window.innerWidth : 1024);
const isLiked = ref(false);
const isFollowing = ref(false);
const likeCount = ref(0);

const updateDimensions = () => {
    if (process.client) {
        windowWidth.value = window.innerWidth;
    }
};

const toggleLike = () => {
    isLiked.value = !isLiked.value;
    likeCount.value += isLiked.value ? 1 : -1;
};

const toggleFollow = () => {
    isFollowing.value = !isFollowing.value;
};

const shareContent = () => {
    // Implémentez votre logique de partage ici
    console.log("Partager le contenu");
};

onMounted(() => {
    if (process.client) {
        window.addEventListener('resize', updateDimensions);
        updateDimensions();
    }
});

onBeforeUnmount(() => {
    if (process.client) {
        window.removeEventListener('resize', updateDimensions);
    }
});

const itemsPerSlide = computed(() => {
    if (windowWidth.value <= 480) return 3;
    if (windowWidth.value <= 768) return 3;
    return 1;
});

const itemWidth = computed(() => {
    return `${100 / itemsPerSlide.value}%`;
});

const slideGroups = computed(() => {
    const groups = [];
    for (let i = 0; i < slides.value.length; i += itemsPerSlide.value) {
        groups.push(slides.value.slice(i, i + itemsPerSlide.value));
    }
    return groups;
});
</script>

<style scoped>
.card {
    border-radius: 12px;
    overflow: hidden;
}

.carousel {
    min-height: 300px;
    position: relative;
}

.carousel-inner {
    height: auto;
    overflow: hidden;
}

.slide-item {
    padding: 0 8px;
    background-color: #ffff;
}

.btn-action {
    padding: 0.5rem 0.8rem;
    border: none;
    background-color: transparent;
    transition: all 0.2s ease;
    position: relative;
    border-radius: 8px;
}

.btn-action:hover {
    background-color: rgba(0, 0, 0, 0.05);
    transform: translateY(-1px);
}

.action-icon {
    font-size: 1.1rem;
    transition: transform 0.2s ease;
}

.btn-action:hover .action-icon {
    transform: scale(1.1);
}

.action-text {
    font-size: 0.85rem;
    margin-left: 0.3rem;
}

.btn-primary {
    background-color: #ffa500;
    border-color: #ffa500;
}

.btn-primary:hover {
    background-color: #e69500;
    border-color: #e69500;
}

.dropdown-menu {
    border: none;
    min-width: 180px;
    border-radius: 8px;
}

.carousel-control-prev-icon,
.carousel-control-next-icon {
    background-size: 1.2rem;
    opacity: 0.9;
}

@media (max-width: 768px) {
    .action-text {
        display: none;
    }

    .btn-action {
        padding: 0.5rem;
    }

    .slide-item {
        padding: 0 6px;
    }

    img.img {
        border-radius: 25px;
    }
}

@media (max-width: 480px) {
    .slide-item {
        padding: 0 4px;
    }
}
</style>