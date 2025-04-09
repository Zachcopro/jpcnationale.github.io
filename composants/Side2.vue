<template>
    <div class="side2 mb-5">
        <div class="info border bg-white p-4 mb-4">
            <p class="">La Région 4 compte 4 circonscriptions, 23 secteurs, 43 localités, 400 jeunes
                actifs...</p>
        </div>
        <div class="d-flex flex-column flex-shrink-0 border bg-white p-4 mb-4">
            <div class="title d-flex justify-content-between">
                <h5>Organigramme</h5>
                <NuxtLink to="/" class="p-1 text-secondary fs-6 text-decoration-none">
                    voir
                </NuxtLink>
            </div>
            <ul class="nav nav-pills flex-column mb-auto">
                <li class="nav-item">
                    <NuxtLink href="/" class="nav-link link-dark" aria-current="page">
                        <i class="bi bi-people bg-light"></i>
                        Bureau Régional 8 membres
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-people bg-light"></i>
                        Bureau Circonscription 5 bureaux
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-people bg-light"></i>
                        Bureau Secteur 23 bureaux
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-people bg-light"></i>
                        Bureau Localité 45 bureaux
                    </NuxtLink>
                </li>
            </ul>
        </div>
        <div class="d-flex flex-column flex-shrink-0 border bg-white p-4 mb-4">
            <div class="title d-flex justify-content-between">
                <h5>Quiz et Jeux</h5>
                <NuxtLink to="/" class="p-1 text-secondary fs-6 text-decoration-none">
                    voir
                </NuxtLink>
            </div>
            <ul class="nav nav-pills flex-column mb-auto">
                <li class="nav-item">
                    <NuxtLink href="/" class="nav-link link-dark" aria-current="page">
                        <i class="bi bi-book bg-light jeux"></i>
                        Jeux Biblique et Classement
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-alphabet-uppercase bg-light jeux"></i>
                        Mots croisés
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-music-note-beamed bg-light jeux"></i>
                        Karaoké
                    </NuxtLink>
                </li>
                <li>
                    <NuxtLink href="#" class="nav-link link-dark">
                        <i class="bi bi-person-workspace bg-light jeux"></i>
                        Personnage
                    </NuxtLink>
                </li>
            </ul>
        </div>
        <div class="d-flex flex-column flex-shrink-0 border bg-white p-4 mb-5">
            <div class="title d-flex justify-content-between">
                <h5>Carrière</h5>
                <NuxtLink to="/" class="p-1 text-secondary fs-6 text-decoration-none">
                    <i class="bi bi-arrow-right-circle"></i>
                </NuxtLink>
            </div>
            <ul class="nav nav-pills flex-column mb-auto">

            </ul>
        </div>
        <div class="div"></div>
    </div>
</template>

<script setup>

</script>

<style scoped>
.bi-people {
    border-radius: 50%;
    padding: 8px 10px;
    margin-right: 5px;
    /* opacity: .7; */
}

.div {
    height: 300px;
}

.jeux {
    border-radius: 50%;
    padding: 8px 10px;
    margin-right: 5px;
}


.side2 {
    position: sticky;
    top: 14%;
    height: 100vh;
    overflow: hidden;
}

.side2:hover {
    overflow: auto;
    transition: .3s ease-in;
}

.side2::-webkit-scrollbar {
    width: 5px;
}

.side2::-webkit-scrollbar-thumb {
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 3px;
}

.side2::-webkit-scrollbar-thumb:hover {
    background-color: rgba(0, 0, 0, 0.5);
}

ul li {
    font-size: .9rem;
}
</style>