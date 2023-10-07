<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
</script>

<!-- eslint-disable vue/no-multiple-template-root -->
<template>
  <Navbar></Navbar>
  <img alt="Vue logo" src="./assets/logo.png" />
  <router-view />
  <Footer></Footer>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
