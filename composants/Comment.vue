<template>
    <div class="d-flex justify-content-between mb-5">
        <div class="user d-flex">
            <img src="" class="rounded-circle bg-white border">
            <span class="fw-bold mx-4">{{ commentaire.autheur }}</span>
        </div>
        <div class="Text bg-light">
            <p class="p-3">{{ commentaire.text }}</p>
        </div>
    </div>
</template>

<script setup>
const props = defineProps(
    { commentaire: Object }
)
</script>

<style scoped>
.Text {
    border-radius: 20px;
    flex: 4;
}

.user {
    flex: 1;
}

.user img {
    padding: 1px 1px;
    width: 3rem;
    height: 3rem;
}
</style>