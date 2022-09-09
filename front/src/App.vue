<script setup>
import HeaderComp from "@/components/template/HeaderComp.vue";
</script>

<template>
  <HeaderComp />
  <main>
    <RouterView />
  </main>
  <FooterComp />
</template>

<style>
@import "@/assets/base.css";
#app {
  max-width: auto;
  margin: 0 auto;
  height: 60vh;

  font-weight: normal;
}
main {
  min-height: 70%;
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
