<template>
    <header class="header sticky-top shadow-sm">
        <div class="container-fluid bg-white py-2">
            <!-- Version Desktop/Tablette -->
            <div class="d-none d-md-flex flex-wrap align-items-center justify-content-between">
                <div class="d-flex align-items-center">
                    <NuxtLink to="/" class="d-flex align-items-center text-decoration-none">
                        <img class="logo-img" src="/logo.jpg" alt="Logo" />
                    </NuxtLink>
                    <div class="search-box ms-3 position-relative">
                        <i class="bi bi-search search-icon"></i>
                        <input type="search" class="form-control search-input ps-4" placeholder="Rechercher..."
                            aria-label="Search" />
                    </div>
                </div>
                <nav class="main-nav d-none d-md-flex mx-auto">
                    <ul class="nav-list d-flex gap-2 mb-0">
                        <li v-for="(item, index) in navItems" :key="index">
                            <NuxtLink :to="item.path"
                                class="nav-link d-flex flex-column align-items-center position-relative"
                                :class="{ 'active': $route.path === item.path }">
                                <i class="bi fs-4" :class="item.icon"></i>
                                <span v-if="item.badge" class="badge bg-danger position-absolute translate-middle">{{
                                    item.badge
                                    }}</span>
                                <span class="nav-text small">{{ item.text }}</span>
                            </NuxtLink>
                        </li>
                    </ul>
                </nav>
                <div class="dropdown ms-3">
                    <a href="#" class="d-flex align-items-center text-decoration-none dropdown-toggle"
                        data-bs-toggle="dropdown" aria-expanded="false">
                        <img src="/userProfil.jpg" alt="Profil" width="32" height="32" class="rounded-circle me-2">
                        <span class="user-name">{{ user }}</span>
                    </a>
                    <ul class="dropdown-menu dropdown-menu-end">
                        <li>
                            <NuxtLink class="dropdown-item" to="/profile"><i class="bi bi-person me-2"></i>Mon Profil
                            </NuxtLink>
                        </li>
                        <li>
                            <NuxtLink class="dropdown-item" to="/settings"><i class="bi bi-gear me-2"></i>Paramètres
                            </NuxtLink>
                        </li>
                        <li>
                            <hr class="dropdown-divider">
                        </li>
                        <li><a class="dropdown-item" href="#"><i class="bi bi-box-arrow-right me-2"></i>Déconnexion</a>
                        </li>
                    </ul>
                </div>
            </div>

            <!-- Version Mobile -->
            <div class="d-md-none">
                <div class="d-flex align-items-center justify-content-between mb-2">
                    <NuxtLink to="/" class="d-flex align-items-center text-decoration-none">
                        <img class="logo-img" src="/logo.jpg" alt="Logo" />
                    </NuxtLink>
                    <div class="search-box mx-2 position-relative flex-grow-1">
                        <i class="bi bi-search search-icon"></i>
                        <input type="search" class="form-control search-input ps-4" placeholder="Rechercher..."
                            aria-label="Search" />
                    </div>
                    <button class="btn btn-menu" @click="toggleMobileMenu" aria-expanded="false"
                        aria-label="Menu principal">
                        <i class="bi bi-list fs-3"></i>
                    </button>
                </div>
                <nav class="mb-2">
                    <ul class="nav-list d-flex justify-content-around mb-0">
                        <li v-for="(item, index) in navItems" :key="index">
                            <NuxtLink :to="item.path"
                                class="nav-link d-flex flex-column align-items-center position-relative"
                                :class="{ 'active': $route.path === item.path }">
                                <i class="bi fs-1" :class="item.icon"></i>
                                <span v-if="item.badge"
                                    class="badge bg-danger position-absolute top-0 end-0 translate-middle">{{ item.badge
                                    }}</span>
                            </NuxtLink>
                        </li>
                    </ul>
                </nav>
                <div class="d-flex justify-content-end">
                    <div class="dropdown">
                        <a href="#" class="d-flex align-items-center text-decoration-none dropdown-toggle"
                            data-bs-toggle="dropdown" aria-expanded="false">
                            <img src="/userProfil.jpg" alt="Profil" width="32" height="32" class="rounded-circle me-2">
                        </a>
                        <ul class="dropdown-menu dropdown-menu-end">
                            <li>
                                <NuxtLink class="dropdown-item" to="/profile"><i class="bi bi-person me-2"></i>Mon
                                    Profil</NuxtLink>
                            </li>
                            <li>
                                <NuxtLink class="dropdown-item" to="/settings"><i class="bi bi-gear me-2"></i>Paramètres
                                </NuxtLink>
                            </li>
                            <li>
                                <hr class="dropdown-divider">
                            </li>
                            <li><a class="dropdown-item" href="#"><i
                                        class="bi bi-box-arrow-right me-2"></i>Déconnexion</a></li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<script setup>
import { ref } from 'vue';
const user = ref('Region 4');
const mobileMenuOpen = ref(false);
const navItems = ref([
    { icon: 'bi-house-door-fill', text: 'Accueil', path: '/', badge: '99+' },
    { icon: 'bi-people-fill', text: 'Amis', path: '/amis' },
    { icon: 'bi-chat-dots-fill', text: 'Messages', path: '/messages', badge: 15 },
    { icon: 'bi-globe-europe-africa', text: 'Nouveautés', path: '/nouveautes', badge: '99+' },
    { icon: 'bi-question-circle-fill', text: 'Aide', path: '/aide' }
]);
const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value;
};
</script>

<style scoped>
.header {
    z-index: 1030;
    background-color: white;
}

li {
    list-style-type: none !important;
    margin-left: 10px;
    margin-right: 10px;
}

.logo-img {
    height: 70px;
    width: auto;
}

.search-box {
    position: relative;
    width: 240px;
}

.search-icon {
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
    color: #6c757d;
    z-index: 10;
}

.search-input {
    padding-left: 40px;
    border-radius: 20px;
    background-color: #f0f2f5;
    border: none;
    height: 40px;
}

.search-input:focus {
    background-color: white;
    box-shadow: 0 0 0 2px #e7f3ff;
}

.nav-link {
    color: #65676b;
    padding: 8px 12px;
    border-radius: 8px;
    transition: all 0.2s;
    position: relative;
}

.nav-link:hover,
.nav-link.active {
    background-color: #f0f2f5;
    color: #1877f2;
}

.nav-link.active .bi {
    color: #1877f2;
}

.nav-text {
    font-size: 0.75rem;
    margin-top: 2px;
}

.user-name {
    font-weight: 500;
    color: #050505;
}

.badge {
    font-size: 0.6rem;
    padding: 2px 4px;
    top: 20%;
    right: 0;
}

.btn-menu {
    color: #050505;
}

.dropdown-menu {
    border: none;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.dropdown-item {
    padding: 8px 16px;
}

.dropdown-item:hover {
    background-color: #f0f2f5;
}

@media (max-width: 992px) {
    .search-box {
        width: 180px;
    }
}

@media (max-width: 768px) {
    .search-box {
        width: 150px;
    }

    .nav-text {
        display: none;
    }

    .nav-list {
        padding: 0;
    }
}

@media (max-width: 576px) {
    .logo-img {
        height: 30px;
    }

    .search-box {
        width: 120px;
    }

    .user-name {
        display: none;
    }
}
</style>