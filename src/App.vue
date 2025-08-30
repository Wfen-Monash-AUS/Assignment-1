
<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-light bg-light border-bottom">
      <div class="container">
        
        <RouterLink to="/" class="navbar-brand d-flex align-items-center">
          <img src="@/assets/logo.svg" alt="Logo" width="28" height="28" class="me-2" />
          <span class="fw-semibold">Health Promotion</span>
        </RouterLink>

        
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#mainNav"
          aria-controls="mainNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        
        <div id="mainNav" class="collapse navbar-collapse">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <RouterLink to="/" class="nav-link">Home</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/about" class="nav-link">About</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>

  <main class="py-4">
    <div class="container">
      <RouterView />
    </div>
  </main>

  <footer class="bg-light border-top py-3 mt-auto">
    <div class="container small text-muted">
      © 2025 Community Sport NFP
    </div>
  </footer>
</template>

<style scoped>
main { min-height: 60vh; }
</style>
