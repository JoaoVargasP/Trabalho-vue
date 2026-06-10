<template>
  <button :class="['ui-button', variant]" :disabled="disabled" @click="$emit('click')">
    <slot />
  </button>
</template>

<script>
export default {
  name: 'UiButton',
  props: {
    variant: { type: String, default: 'primary' },
    disabled: { type: Boolean, default: false }
  }
}
</script>

<style scoped>
.ui-button {
  padding: 0.6rem 1rem;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-weight: 600;
}
.ui-button.primary { background:#2b6cb0; color:white; }
.ui-button.secondary { background:#edf2f7; color:#2d3748; }
.ui-button:disabled { opacity:0.6; cursor:not-allowed; }
</style>
