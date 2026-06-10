<template>
  <div v-if="visible" class="overlay" @click.self="close">
    <div class="modal">
      <header><slot name="header">Título</slot></header>
      <main><slot /></main>
      <footer>
        <ui-button @click="close">Fechar</ui-button>
        <ui-button variant="secondary" @click="$emit('confirm')">Confirmar</ui-button>
      </footer>
    </div>
  </div>
</template>

<script>
import UiButton from './UiButton.vue'
export default {
  name: 'Modal',
  components: { UiButton },
  props: { visible: { type: Boolean, default: false } },
  methods: {
    close() { this.$emit('update:visible', false) }
  }
}
</script>

<style scoped>
.overlay {
  position: fixed; inset:0; display:flex; align-items:center; justify-content:center;
  background: rgba(0,0,0,0.4); padding:1rem;
}
.modal {
  background:white; border-radius:8px; width:100%; max-width:520px; padding:1rem;
}
.modal header { font-weight:700; margin-bottom:0.5rem; }
.modal footer { display:flex; gap:0.5rem; justify-content:flex-end; margin-top:1rem; }
</style>
