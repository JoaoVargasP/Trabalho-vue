<template>
  <div class="card">
    <div class="card-body">
      <h3>{{ product.name }}</h3>
      <p class="category">{{ product.category }}</p>
      <p class="desc">{{ product.description }}</p>
      <div class="footer">
        <strong>R$ {{ product.price.toFixed(2) }}</strong>
        <ui-button @click="$emit('add', product)">Adicionar</ui-button>
      </div>
    </div>
  </div>
</template>

<script>
import UiButton from './UiButton.vue'
export default {
  name: 'CardProduct',
  components: { UiButton },
  props: { product: { type: Object, required: true } }
}
</script>

<style scoped>
.card {
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 1rem;
  background: white;
}
.card-body h3 { margin: 0 0 0.25rem 0; font-size: 1.05rem; }
.category { font-size: 0.85rem; color:#718096; margin-bottom:0.5rem; }
.desc { font-size:0.9rem; color:#4a5568; margin-bottom:0.75rem; }
.footer { display:flex; justify-content:space-between; align-items:center; gap:1rem; }
</style>
