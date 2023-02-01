<template>
  <div id="mensagem-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  props: {
    msg: String,
  },
};
</script>

<style scoped>
#mensagem-container {
  background-color: #40dfef;
  color: #b9f8d3;
  border: 2px solid #fffbe7;
  max-width: 400px;
  margin: 30px auto;
  padding: 14px;
  border-radius: 12px;
}

#mensagem-container p {
  font-weight: bold;
}
</style>
