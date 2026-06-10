<template>
  <div id="app">
    <nav class="navbar">
      <router-link to="/">Home</router-link>
      <router-link to="/catalog">Catálogo</router-link>
      <router-link to="/about">Sobre</router-link>
    </nav>

    <!-- Aqui o Vue Router renderiza a página atual -->
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
/* Estilo global simples */
#app {
  font-family: Inter, system-ui, sans-serif;
  color: #1a202c;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.navbar {
  display: flex;
  gap: 1rem;
  background: #2b6cb0;
  padding: 1rem;
}

.navbar a {
  color: white;
  font-weight: 600;
}

.navbar a.router-link-active {
  text-decoration: underline;
}
</style>
