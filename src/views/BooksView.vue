<template>
    <div class="books-page">

        <!-- Header -->
        <header class="books-header">
            <h1>📚 Biblioteca Virtual</h1>
            <p class="subtitle">Explorá y gestioná tu colección de libros</p>
        </header>

        <main class="books-main">

            <!-- Formulario para agregar libro -->
            <section class="card form-card">
                <h2>➕ Agregar nuevo libro</h2>
                <form @submit.prevent="agregarLibro" class="book-form">
                    <div class="form-group">
                        <label for="titulo">Título</label>
                        <input id="titulo" v-model.trim="nuevoLibro.titulo" type="text" placeholder="Ej: Don Quijote"
                            required />
                    </div>
                    <div class="form-group">
                        <label for="autor">Autor</label>
                        <input id="autor" v-model.trim="nuevoLibro.autor" type="text"
                            placeholder="Ej: Miguel de Cervantes" required />
                    </div>
                    <div class="form-group">
                        <label for="categoria">Categoría</label>
                        <select id="categoria" v-model="nuevoLibro.categoria" required>
                            <option value="" disabled>Seleccionar categoría</option>
                            <option v-for="cat in categorias" :key="cat" :value="cat">{{ cat }}</option>
                        </select>
                    </div>
                    <button type="submit" class="btn btn-primary">Agregar libro</button>
                </form>
            </section>

            <!-- Listado de libros -->
            <section class="card list-card">
                <div class="list-header">
                    <h2>📖 Listado de libros</h2>
                    <div class="filter-group">
                        <label for="filtro">Filtrar por categoría:</label>
                        <select id="filtro" v-model="filtroCategoria">
                            <option value="">Todas</option>
                            <option v-for="cat in categorias" :key="cat" :value="cat">{{ cat }}</option>
                        </select>
                    </div>
                </div>

                <p v-if="librosFiltrados.length === 0" class="empty-msg">
                    No hay libros en esta categoría.
                </p>

                <ul v-else class="books-list">
                    <li v-for="libro in librosFiltrados" :key="libro.id" class="book-item">
                        <div class="book-info">
                            <span class="book-title">{{ libro.titulo }}</span>
                            <span class="book-author">{{ libro.autor }}</span>
                            <span class="badge">{{ libro.categoria }}</span>
                        </div>
                        <button class="btn btn-danger" @click="eliminarLibro(libro.id)" title="Eliminar">
                            🗑️
                        </button>
                    </li>
                </ul>

                <p class="total">Total: <strong>{{ librosFiltrados.length }}</strong> libro(s)</p>
            </section>

        </main>
    </div>
</template>


<script setup>
import { ref, computed } from 'vue';

// ─── Estado ───────────────────────────────────────────────
const categorias = ['Ficción', 'Fábula', 'Distopía', 'No ficción', 'Thriller', 'Ciencia', 'Historia'];

const libros = ref([
    { id: 1, titulo: 'Cien años de soledad', autor: 'Gabriel García Márquez', categoria: 'Ficción' },
    { id: 2, titulo: 'El principito', autor: 'Antoine de Saint-Exupéry', categoria: 'Fábula' },
    { id: 3, titulo: '1984', autor: 'George Orwell', categoria: 'Distopía' },
    { id: 4, titulo: 'Sapiens', autor: 'Yuval Noah Harari', categoria: 'No ficción' },
    { id: 5, titulo: 'El código Da Vinci', autor: 'Dan Brown', categoria: 'Thriller' },
]);

const nuevoLibro = ref({ titulo: '', autor: '', categoria: '' });
const filtroCategoria = ref('');

// ─── Computed ─────────────────────────────────────────────
const librosFiltrados = computed(() =>
    filtroCategoria.value
        ? libros.value.filter(l => l.categoria === filtroCategoria.value)
        : libros.value
);

// ─── Métodos ──────────────────────────────────────────────
let nextId = 6;

function agregarLibro() {
    libros.value.push({ id: nextId++, ...nuevoLibro.value });
    nuevoLibro.value = { titulo: '', autor: '', categoria: '' };
}

function eliminarLibro(id) {
    libros.value = libros.value.filter(l => l.id !== id);
}
</script>


<style scoped>
/* ── Variables ── */
:root {
    --primary: #6c63ff;
    --danger: #e74c3c;
    --bg: #f0f2ff;
    --card: #ffffff;
    --text: #2d2d3a;
    --muted: #7a7a9d;
    --radius: 14px;
    --shadow: 0 4px 20px rgba(108, 99, 255, 0.12);
}

/* ── Página ── */
.books-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f0f2ff 0%, #e8ecff 100%);
    font-family: 'Segoe UI', system-ui, sans-serif;
    color: var(--text);
    padding-bottom: 3rem;
}

/* ── Header ── */
.books-header {
    background: linear-gradient(135deg, #6c63ff, #a78bfa);
    color: #fff;
    text-align: center;
    padding: 2.5rem 1rem 2rem;
    margin-bottom: 2rem;
}

.books-header h1 {
    font-size: 2.2rem;
    font-weight: 700;
    margin: 0 0 0.4rem;
}

.subtitle {
    font-size: 1rem;
    opacity: 0.88;
    margin: 0;
}

/* ── Main layout ── */
.books-main {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    max-width: 960px;
    margin: 0 auto;
    padding: 0 1.2rem;
}

@media (max-width: 700px) {
    .books-main {
        grid-template-columns: 1fr;
    }
}

/* ── Card base ── */
.card {
    background: var(--card);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 1.6rem;
}

.card h2 {
    font-size: 1.15rem;
    font-weight: 700;
    margin: 0 0 1.2rem;
    color: #6c63ff;
}

/* ── Formulario ── */
.book-form {
    display: flex;
    flex-direction: column;
    gap: 0.9rem;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
}

.form-group label {
    font-size: 0.82rem;
    font-weight: 600;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.04em;
}

.form-group input,
.form-group select {
    padding: 0.55rem 0.85rem;
    border: 1.5px solid #d1d5f5;
    border-radius: 8px;
    font-size: 0.95rem;
    color: var(--text);
    background: #fafaff;
    outline: none;
    transition: border-color 0.2s;
}

.form-group input:focus,
.form-group select:focus {
    border-color: #6c63ff;
    background: #fff;
}

/* ── Botones ── */
.btn {
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 600;
    transition: opacity 0.18s, transform 0.15s;
}

.btn:hover {
    opacity: 0.88;
    transform: translateY(-1px);
}

.btn:active {
    transform: translateY(0);
}

.btn-primary {
    background: linear-gradient(135deg, #6c63ff, #a78bfa);
    color: #fff;
    padding: 0.65rem 1.4rem;
    font-size: 0.95rem;
    margin-top: 0.3rem;
}

.btn-danger {
    background: #fdecea;
    color: var(--danger);
    padding: 0.4rem 0.7rem;
    font-size: 1rem;
    flex-shrink: 0;
}

/* ── Filtro ── */
.list-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 0.6rem;
    margin-bottom: 1rem;
}

.list-header h2 {
    margin: 0;
}

.filter-group {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.82rem;
}

.filter-group label {
    color: var(--muted);
    font-weight: 600;
}

.filter-group select {
    padding: 0.35rem 0.7rem;
    border: 1.5px solid #d1d5f5;
    border-radius: 8px;
    font-size: 0.85rem;
    outline: none;
    cursor: pointer;
    color: var(--text);
}

/* ── Lista de libros ── */
.books-list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 0.7rem;
}

.book-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.8rem;
    padding: 0.75rem 1rem;
    border-radius: 10px;
    background: #f7f8ff;
    border: 1px solid #e8eaff;
    transition: box-shadow 0.18s;
}

.book-item:hover {
    box-shadow: 0 2px 10px rgba(108, 99, 255, 0.15);
}

.book-info {
    display: flex;
    flex-direction: column;
    gap: 0.15rem;
}

.book-title {
    font-weight: 700;
    font-size: 0.95rem;
}

.book-author {
    font-size: 0.82rem;
    color: var(--muted);
}

.badge {
    display: inline-block;
    background: #ede9ff;
    color: #6c63ff;
    font-size: 0.73rem;
    font-weight: 700;
    padding: 0.18rem 0.6rem;
    border-radius: 20px;
    margin-top: 0.2rem;
    text-transform: uppercase;
    letter-spacing: 0.04em;
}

/* ── Footer info ── */
.empty-msg {
    text-align: center;
    color: var(--muted);
    padding: 1.5rem 0;
    font-style: italic;
}

.total {
    text-align: right;
    font-size: 0.85rem;
    color: var(--muted);
    margin: 1rem 0 0;
}
</style>
