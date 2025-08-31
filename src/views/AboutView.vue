<script setup>
import { ref, reactive, onMounted } from 'vue';

const STORAGE_KEY = 'hp_registrations';


const programs = ref([
  { id: 1, name: 'Social Badminton', level: 'Beginner', location: 'Clayton', slots: 12 },
  { id: 2, name: 'Walking Group', level: 'All',      location: 'Bentleigh', slots: 20 },
  { id: 3, name: 'Low-impact Yoga', level: 'Beginner', location: 'Oakleigh', slots: 15 },
]);


const form = reactive({
  name: '',
  email: '',
  programId: '', 
});


const errors = reactive({
  name: '',
  email: '',
  programId: '',
});


const registrations = ref([]);


function load() {
  const raw = localStorage.getItem(STORAGE_KEY);
  registrations.value = raw ? JSON.parse(raw) : [];
}


function save() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(registrations.value));
}


function validate() {
  errors.name = form.name.trim() ? '' : 'Name is required.';
  errors.programId = form.programId ? '' : 'Please choose a program.';

  const emailOk = /^\S+@\S+\.\S+$/.test(form.email);
  errors.email = emailOk ? '' : 'Email is invalid.';

  return !(errors.name || errors.email || errors.programId);
}


function submitForm() {
  if (!validate()) return;

  const selected = programs.value.find(p => p.id === Number(form.programId));
  registrations.value.push({
    name: form.name.trim(),
    email: form.email.trim(),
    programName: selected ? selected.name : '',
    at: new Date().toISOString(),
  });
  save();

  form.name = '';
  form.email = '';
  form.programId = '';
}


function clearAll() {
  if (confirm('Clear all saved registrations?')) {
    registrations.value = [];
    save();
  }
}

onMounted(load);
</script>

<template>
  <div class="row g-4">

    <div class="col-12 col-lg-6">
      <h2 class="h5 mb-3">Available Programs</h2>
      <ul class="list-group">
        <li
          v-for="p in programs"
          :key="p.id"
          class="list-group-item d-flex justify-content-between align-items-center"
        >
          <div>
            <div class="fw-semibold">{{ p.name }}</div>
            <small class="text-muted">{{ p.level }} • {{ p.location }}</small>
          </div>
          <span class="badge bg-secondary">{{ p.slots }} slots</span>
        </li>
      </ul>
    </div>

    <div class="col-12 col-lg-6">
      <h2 class="h5 mb-3">Quick Registration</h2>

      <form @submit.prevent="submitForm" novalidate>
        <div class="mb-3">
          <label class="form-label">Name</label>
          <input v-model="form.name" type="text" class="form-control" placeholder="e.g., Olivia Smith" />
          <div class="text-danger small" v-if="errors.name">{{ errors.name }}</div>
        </div>

        <div class="mb-3">
          <label class="form-label">Email</label>
          <input v-model="form.email" type="email" class="form-control" placeholder="name@example.com" />
          <div class="text-danger small" v-if="errors.email">{{ errors.email }}</div>
        </div>

        <div class="mb-3">
          <label class="form-label">Choose a program</label>
          <select v-model="form.programId" class="form-select">
            <option value="">-- please choose --</option>
            <option v-for="p in programs" :key="p.id" :value="p.id">{{ p.name }}</option>
          </select>
          <div class="text-danger small" v-if="errors.programId">{{ errors.programId }}</div>
        </div>

        <button type="submit" class="btn btn-primary">Register</button>
      </form>
    </div>
  </div>

  <hr class="my-4" />


  <div>
    <div class="d-flex align-items-center justify-content-between">
      <h2 class="h5 mb-0">Saved Registrations</h2>
      <button @click="clearAll" class="btn btn-outline-danger btn-sm">Clear all</button>
    </div>

    <div class="table-responsive mt-3" v-if="registrations.length">
      <table class="table table-sm align-middle">
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Program</th>
            <th>Saved at</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(r, i) in registrations" :key="i">
            <td>{{ r.name }}</td>
            <td>{{ r.email }}</td>
            <td>{{ r.programName }}</td>
            <td>{{ new Date(r.at).toLocaleString() }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p v-else class="text-muted">No registrations yet.</p>
  </div>
</template>
