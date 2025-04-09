<template>
    <div class="bg-light">
        <div class="row mt-3">
            <div class="side">
                <Side1 />
            </div>
            <div class="mainContain">
                <SubMain />
            </div>
        </div>
    </div>
</template>

<script setup>
import Side1 from '~/composants/Side1.vue';
import SubMain from './SubMain.vue';
</script>

<style scoped>
.side {
    /* padding-left: 2rem; */
    flex: 1;
}

.mainContain {
    flex: 4;
}

/* responsive */

@media (max-width: 820px) {
    .side {
        display: none !important;
    }
}

@media (max-width: 750px) {
    .mainContain {
        width: 95%;
    }
}
</style>