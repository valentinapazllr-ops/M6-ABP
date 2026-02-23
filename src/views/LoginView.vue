<template>
    <div class="login-page">
        <div class="login-card">

            <div class="login-logo">📚</div>
            <h1 class="login-title">LibroApp</h1>
            <p class="login-sub">Iniciá sesión para acceder a tu biblioteca</p>

            <form @submit.prevent="handleLogin" class="login-form">

                <div class="form-group">
                    <label for="email">Correo electrónico</label>
                    <input id="email" v-model.trim="email" type="email" placeholder="usuario@email.com"
                        autocomplete="email" required />
                </div>

                <div class="form-group">
                    <label for="password">Contraseña</label>
                    <div class="password-wrapper">
                        <input id="password" v-model="password" :type="showPassword ? 'text' : 'password'"
                            placeholder="••••••••" autocomplete="current-password" required />
                        <button type="button" class="toggle-pass" @click="showPassword = !showPassword">
                            {{ showPassword ? '🙈' : '👁️' }}
                        </button>
                    </div>
                </div>

                <p v-if="error" class="error-msg">⚠️ {{ error }}</p>

                <button type="submit" class="btn-login" :disabled="loading">
                    <span v-if="loading">Ingresando…</span>
                    <span v-else>Ingresar →</span>
                </button>

            </form>

            <p class="demo-hint">
                Ingresá cualquier email y una contraseña de al menos 4 caracteres.
            </p>

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const email = ref('');
const password = ref('');
const error = ref('');
const loading = ref(false);
const showPassword = ref(false);

function handleLogin() {
    error.value = '';

    // Validar contraseña mínima
    if (password.value.length < 4) {
        error.value = 'La contraseña debe tener al menos 4 caracteres.';
        return;
    }

    loading.value = true;

    // Simula espera de red y da acceso con cualquier credencial válida
    setTimeout(() => {
        localStorage.setItem('libroapp_auth', 'true');
        router.push('/');
        loading.value = false;
    }, 700);
}
</script>

<style scoped>
/* ── Página ── */
.login-page {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #f0f2ff 0%, #dde1ff 100%);
    font-family: 'Segoe UI', system-ui, sans-serif;
    padding: 1.5rem;
}

/* ── Card ── */
.login-card {
    background: #fff;
    border-radius: 20px;
    box-shadow: 0 8px 40px rgba(108, 99, 255, 0.15);
    padding: 2.5rem 2.2rem;
    width: 100%;
    max-width: 400px;
    text-align: center;
}

.login-logo {
    font-size: 3rem;
    margin-bottom: 0.4rem;
}

.login-title {
    font-size: 1.9rem;
    font-weight: 800;
    color: #2d2d3a;
    margin: 0 0 0.3rem;
}

.login-sub {
    font-size: 0.9rem;
    color: #7a7a9d;
    margin: 0 0 1.8rem;
}

/* ── Formulario ── */
.login-form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    text-align: left;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
}

.form-group label {
    font-size: 0.8rem;
    font-weight: 700;
    color: #7a7a9d;
    text-transform: uppercase;
    letter-spacing: 0.04em;
}

.form-group input {
    width: 100%;
    padding: 0.65rem 0.9rem;
    border: 1.5px solid #d1d5f5;
    border-radius: 10px;
    font-size: 0.95rem;
    color: #2d2d3a;
    background: #fafaff;
    outline: none;
    transition: border-color 0.2s;
    box-sizing: border-box;
}

.form-group input:focus {
    border-color: #6c63ff;
    background: #fff;
}

/* ── Campo contraseña ── */
.password-wrapper {
    position: relative;
}

.password-wrapper input {
    padding-right: 2.8rem;
}

.toggle-pass {
    position: absolute;
    right: 0.65rem;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1rem;
    line-height: 1;
}

/* ── Error ── */
.error-msg {
    color: #e74c3c;
    font-size: 0.85rem;
    background: #fdecea;
    padding: 0.55rem 0.9rem;
    border-radius: 8px;
    margin: 0;
}

/* ── Botón ── */
.btn-login {
    background: linear-gradient(135deg, #6c63ff, #a78bfa);
    color: #fff;
    border: none;
    border-radius: 10px;
    padding: 0.75rem;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    transition: opacity 0.2s, transform 0.15s;
    margin-top: 0.3rem;
}

.btn-login:hover:not(:disabled) {
    opacity: 0.88;
    transform: translateY(-2px);
}

.btn-login:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

/* ── Hint demo ── */
.demo-hint {
    font-size: 0.8rem;
    color: #7a7a9d;
    margin-top: 1.4rem;
    background: #f3f4ff;
    border-radius: 8px;
    padding: 0.5rem 0.8rem;
}
</style>