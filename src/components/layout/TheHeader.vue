<template>
  <header>
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: ['title'],
};
</script>

<style scoped>
header {
  width: 100%;
  height: 5rem;
  background-color: #640032;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  color: #fff;
  /* padding: 2rem 0; */
  /* margin-bottom: 2rem; */
  margin: 0;
}
</style>
