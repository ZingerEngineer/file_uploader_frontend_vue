<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="wrapper">
    <header>
      <div class="title-wrapper">
        <p class="title">File uploader.</p>
        <img alt="file uploader logo" class="logo" src="@/assets/logo.svg" />
      </div>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </header>

    <RouterView />
  </div>
</template>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  padding: 0px;
}

.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.title-wrapper {
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
}
.title {
  font-size: 8rem;
}

.logo {
  width: 10rem;
}
nav {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 100%;
  font-size: 20px;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>
