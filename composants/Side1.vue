<template>
    <div class="side1 d-flex flex-column flex-shrink-0 position-sticky p-4 bg-light">
        <div class="logo">
            <img src="/logo EMEC.jpg" alt="" class="w-75">
        </div>
        <div class="userConnect my-4">
            <span class="fs-4 fw-medium">{{ user }}</span>
            <span class="d-block opacity-50">@jpcregion 4</span>
        </div>
        <ul class="nav nav-pills flex-column mb-5">
            <li class="nav-item">
                <NuxtLink href="/" class="nav-link link-dark" aria-current="page">
                    Accueil
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Organigramme
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Médiathèque
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Quiz et Jeux
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Camp des Jeunes
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Projets
                </NuxtLink>
            </li>
            <li>
                <NuxtLink href="#" class="nav-link link-dark">
                    Carrière
                </NuxtLink>
            </li>
        </ul>
        <NuxtLink to="/" class="btn btnNewPage rounded">
            Créé une page
        </NuxtLink>
    </div>
</template>

<script setup>
const user = ref('JPC région 4')
</script>

<style>
/* .position-sticky {
    top: -1%;
} */
.side1 {
    top: -20%;
    height: 100vh;
    overflow: hidden;
}

.side1:hover {
    overflow: auto;
    transition: .3s ease-in;
}

.side1::-webkit-scrollbar {
    width: 1px;
}

.active {
    background-color: orange !important;
}

.btnNewPage {
    background-color: orange;
    color: white;
    width: 10rem;
}

.nav-link:hover {
    background-color: rgb(255, 165, 0, 0.2);
    /* transform: translateX(3px); */
    transition: .2s ease-in;
}
</style>