<template>
  <form @submit.prevent="onSubmit" class="form">
    <label>
      Nome
      <input v-model="form.name" required />
    </label>

    <label>
      Email
      <input v-model="form.email" type="email" required />
      <small v-if="emailError" class="error">Email inválido</small>
    </label>

    <label>
      Mensagem
      <textarea v-model="form.message" rows="4"></textarea>
    </label>

    <div class="actions">
      <ui-button :disabled="submitting" type="submit">Enviar</ui-button>
      <ui-button variant="secondary" type="button" @click="reset">Limpar</ui-button>
    </div>

    <p v-if="success" class="success">Enviado com sucesso (simulado).</p>
  </form>
</template>

<script>
import UiButton from './UiButton.vue'
export default {
  name: 'FormCadastro',
  components: { UiButton },
  data() {
    return {
      form: { name: '', email: '', message: '' },
      submitting: false,
      success: false
    }
  },
  computed: {
    emailError() {
      return this.form.email && !/^\S+@\S+\.\S+$/.test(this.form.email)
    }
  },
  methods: {
    reset() {
      this.form = { name: '', email: '', message: '' }
      this.success = false
    },
    onSubmit() {
      if (this.emailError) return
      this.submitting = true
      setTimeout(() => {
        this.submitting = false
        this.success = true
        this.$emit('submitted', { ...this.form })
      }, 800)
    }
  }
}
</script>

<style scoped>
.form label { display:block; margin-bottom:0.6rem; font-weight:600; }
.form input, .form textarea { width:100%; padding:0.5rem; border:1px solid #cbd5e0; border-radius:6px; }
.actions { display:flex; gap:0.5rem; margin-top:0.6rem; }
.error { color:#e53e3e; font-size:0.85rem; }
.success { color:#2f855a; margin-top:0.6rem; }
</style>
