<template>
  <section class="container">
    <header class="hero">
      <h1>Bem-vindo à Loja Vue</h1>
      <p>Exemplo de SPA com componentes, busca, formulário e modal.</p>
      <router-link to="/catalog"><ui-button>Ver Catálogo</ui-button></router-link>
    </header>

    <section class="features">
      <div class="card-feature">
        <h3>Responsivo</h3>
        <p>Funciona em desktop, tablet e smartphone.</p>
      </div>
      <div class="card-feature">
        <h3>Interativo</h3>
        <p>Busca em tempo real e formulário com validação.</p>
      </div>
    </section>
  </section>
</template>

<script>
import UiButton from '../components/UiButton.vue'
export default {
  name: 'Home',
  components: { UiButton }
}
</script>

<style scoped>
.container { padding:1rem; max-width:1100px; margin:0 auto; }
.hero { text-align:center; padding:2rem 1rem; }
.features { display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:1rem; margin-top:1.5rem; }
.card-feature { padding:1rem; border:1px solid #e2e8f0; border-radius:8px; background:white; }
</style>
