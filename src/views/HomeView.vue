<template>
  <main class="home">
    <div class="hero">
      <div class="hero-icon">📚</div>
      <h1>Bienvenido a <span class="highlight">LibroApp</span></h1>
      <p class="description">
        Tu biblioteca virtual para explorar, agregar y gestionar tus libros favoritos en un solo lugar.
      </p>
      <RouterLink to="/books" class="cta-btn">Ver catálogo de libros →</RouterLink>
    </div>

    <div class="features">
      <div class="feature-card">
        <span class="icon">🔍</span>
        <h3>Explorá</h3>
        <p>Navegá por el catálogo y descubrí libros por categoría.</p>
      </div>
      <div class="feature-card">
        <span class="icon">➕</span>
        <h3>Agregá</h3>
        <p>Sumá tus libros favoritos a la colección fácilmente.</p>
      </div>
      <div class="feature-card">
        <span class="icon">🗂️</span>
        <h3>Organizá</h3>
        <p>Filtrá y gestioná tu lista con un clic.</p>
      </div>
    </div>
  </main>
</template>

<script setup>
import { RouterLink } from 'vue-router';
</script>

<style scoped>
.home {
  min-height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem 1.5rem;
  background: linear-gradient(135deg, #f0f2ff 0%, #e8ecff 100%);
  font-family: 'Segoe UI', system-ui, sans-serif;
}

/* ── Hero ── */
.hero {
  text-align: center;
  max-width: 560px;
  margin-bottom: 3rem;
}

.hero-icon {
  font-size: 3.5rem;
  margin-bottom: 0.8rem;
}

.hero h1 {
  font-size: 2.4rem;
  font-weight: 800;
  color: #2d2d3a;
  margin: 0 0 1rem;
}

.highlight {
  color: #6c63ff;
}

.description {
  font-size: 1.05rem;
  color: #7a7a9d;
  line-height: 1.6;
  margin-bottom: 1.8rem;
}

.cta-btn {
  display: inline-block;
  background: linear-gradient(135deg, #6c63ff, #a78bfa);
  color: #fff;
  text-decoration: none;
  padding: 0.75rem 2rem;
  border-radius: 50px;
  font-weight: 700;
  font-size: 1rem;
  transition: opacity 0.2s, transform 0.15s;
}

.cta-btn:hover {
  opacity: 0.88;
  transform: translateY(-2px);
}

/* ── Features ── */
.features {
  display: flex;
  gap: 1.2rem;
  flex-wrap: wrap;
  justify-content: center;
}

.feature-card {
  background: #fff;
  border-radius: 14px;
  box-shadow: 0 4px 20px rgba(108, 99, 255, 0.1);
  padding: 1.5rem 1.8rem;
  text-align: center;
  width: 190px;
}

.feature-card .icon {
  font-size: 2rem;
  display: block;
  margin-bottom: 0.6rem;
}

.feature-card h3 {
  font-size: 1rem;
  font-weight: 700;
  color: #6c63ff;
  margin: 0 0 0.4rem;
}

.feature-card p {
  font-size: 0.85rem;
  color: #7a7a9d;
  margin: 0;
  line-height: 1.5;
}
</style>