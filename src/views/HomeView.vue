<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <section class="bg-light border-bottom">
    <div class="container py-5">
      <div class="row align-items-center g-4">
        <div class="col-12 col-lg-7">
          <h1 class="display-5 fw-semibold mb-3">
            Move together. Feel better.
          </h1>
          <p class="lead text-muted mb-4">
            Join community sport activities to improve physical and mental wellbeing.
            Simple sign-up. Inclusive for all ages and levels.
          </p>


          <RouterLink to="/about" class="btn btn-primary btn-lg me-2">
            Get started
          </RouterLink>
          <RouterLink to="/about" class="btn btn-outline-secondary btn-lg">
            Browse programs
          </RouterLink>
        </div>

        <div class="col-12 col-lg-5 text-center">
          <img src="@/assets/logo.svg" alt="Community sport logo" width="160" height="160" />
        </div>
      </div>
    </div>
  </section>


  <section class="container py-5">
    <div class="row g-4">
      <div class="col-12 col-md-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Inclusive</h5>
            <p class="card-text text-muted">
              Welcoming beginners, seniors, and families. Low-impact options available.
            </p>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Local & Accessible</h5>
            <p class="card-text text-muted">
              Activities near you with clear directions and step-free options.
            </p>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Simple Sign-up</h5>
            <p class="card-text text-muted">
              Quick registration and reminders to help you keep a healthy routine.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
img { max-width: 100%; height: auto; }
</style>
