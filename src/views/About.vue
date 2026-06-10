<template>
  <section class="container">
    <h2>Sobre</h2>
    <p>Projeto exemplo em Vue.js com componentes, navegação e interatividade.</p>

    <h3>Contato</h3>
    <form-cadastro @submitted="onSubmitted" />
  </section>
</template>

<script>
import FormCadastro from '../components/FormCadastro.vue'
export default {
  name: 'About',
  components: { FormCadastro },
  methods: {
    onSubmitted(data) {
      // Simulação: aqui você poderia enviar para API
      console.log('Form enviado', data)
      alert('Obrigado, ' + data.name + '! Recebemos sua mensagem.')
    }
  }
}
</script>

<style scoped>
.container { padding:1rem; max-width:800px; margin:0 auto; }
</style>
