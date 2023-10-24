<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="row justify-content-center text-center">
    <nav class="navbar navbar-expand-lg" data-bs-theme="black">
      <div class="container-fluid">
        <RouterLink class="navbar-brand text-success" to="/">Navbar</RouterLink>
        <button
          class="navbar-toggler bg-white"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <RouterLink to="/">Home</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/about">About</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/digimons">Digimons</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/favoritos">Favoritos</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div class="container">
      <RouterView />
    </div>
    <footer>Footer</footer>
  </div>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
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
