<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['mode'],
};
</script>

<style scoped>
button {
  background-color: transparent;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: #fff;
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  cursor: pointer;
}
button:active,
button:hover {
  background-color: #270041;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

.flat:hover {
  background-color: #edd2ff;
}
</style>
