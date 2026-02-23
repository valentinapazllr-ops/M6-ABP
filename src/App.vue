<script setup>
import { computed } from 'vue'
import { RouterLink, RouterView, useRouter } from 'vue-router'

const router = useRouter()

const isAuthenticated = computed(() => localStorage.getItem('libroapp_auth') === 'true')

function logout() {
  localStorage.removeItem('libroapp_auth')
  router.push('/login')
}
</script>

<template>
  <nav class="app-nav">
    <span class="nav-brand">📚 LibroApp</span>
    <div class="nav-links">
      <template v-if="isAuthenticated">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/books">Books</RouterLink>
        <button class="btn-logout" @click="logout">Cerrar sesión 🚪</button>
      </template>
      <template v-else>
        <RouterLink to="/login">Login</RouterLink>
      </template>
    </div>
  </nav>

  <RouterView />
</template>

<style scoped>
.app-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.85rem 2rem;
  background: #fff;
  box-shadow: 0 2px 12px rgba(108, 99, 255, 0.1);
  position: sticky;
  top: 0;
  z-index: 100;
  font-family: 'Segoe UI', system-ui, sans-serif;
}

.nav-brand {
  font-weight: 800;
  font-size: 1.1rem;
  color: #6c63ff;
  letter-spacing: 0.01em;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1.2rem;
}

.nav-links a {
  text-decoration: none;
  color: #7a7a9d;
  font-weight: 600;
  font-size: 0.95rem;
  transition: color 0.18s;
}

.nav-links a:hover,
.nav-links a.router-link-active {
  color: #6c63ff;
}

.btn-logout {
  background: #fdecea;
  color: #e74c3c;
  border: none;
  border-radius: 8px;
  padding: 0.4rem 1rem;
  font-size: 0.88rem;
  font-weight: 700;
  cursor: pointer;
  transition: opacity 0.18s, transform 0.15s;
}

.btn-logout:hover {
  opacity: 0.85;
  transform: translateY(-1px);
}
</style>
