<template>
  <div class="searchbar">
    <input
      v-model="query"
      @input="onInput"
      type="search"
      placeholder="Buscar produtos..."
      aria-label="Buscar"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  props: { modelValue: { type: String, default: '' } },
  emits: ['update:modelValue', 'search'],
  data() { return { query: this.modelValue } },
  watch: {
    modelValue(v) { this.query = v }
  },
  methods: {
    onInput() {
      this.$emit('update:modelValue', this.query)
      this.$emit('search', this.query)
    }
  }
}
</script>

<style scoped>
.searchbar input {
  width: 100%;
  padding: 0.6rem 0.8rem;
  border-radius: 8px;
  border: 1px solid #cbd5e0;
}
</style>
