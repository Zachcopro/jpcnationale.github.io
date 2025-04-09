<script setup lang="ts">
import { NuxtPage } from '#components';
import Header from './composants/Header.vue';
// import 'bootstrap/dist/js/bootstrap.bundle.min.js'

const appConfig = useAppConfig();
useSeoMeta({
  title: appConfig.title
})
</script>

<template>
  <div>
    <NuxtLoadingIndicator />
    <NuxtRouteAnnouncer />
    <Header />
    <NuxtPage />
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #F8F9FA;
}
</style>
