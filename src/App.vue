<script setup>
import { RouterLink, RouterView } from 'vue-router'
import './assets/main.css'
</script>

<template>
  <nav class="nav-container">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
    <RouterLink to="/employees">Employees</RouterLink>
  </nav>

  <RouterView />
</template>

<style scoped>
.nav-container {
  display: flex;
  font-family: 'basic-sans', sans-serif;
  font-weight: 700;
  font-size: 14px;
  text-transform: uppercase;
  gap: 40px;
  letter-spacing: 0.1rem;
  line-height: 22.4px;
  align-items: center;
  justify-content: center;
  margin: 0 40px;
  height: 80px;
  max-width: 100%;
}

a {
  text-decoration: none;
  color: black;
}

RouterLink {
  text-decoration: none;
}
</style>
