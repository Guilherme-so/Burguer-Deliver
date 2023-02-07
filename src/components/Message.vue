<template>
  <div
    id="mensagem-container"
    :class="[
      msg.status === 'Criado' ? 'criado'
      : msg.status === 'Atualizado' ? 'atualizado'
      : msg.status === 'Deletado' ? 'deletado' : ''
    ]"
  >
    <p>{{ msg.mensagem }}</p>
  </div>
</template>

<script>
export default {
  props: {
    msg: {
      mensagem: String,
      status: "Criado" || "Atualizado" || "Deletado",
    },
  },
};
</script>

<style scoped>
#mensagem-container {
  color: #FFF;
  border: 2px solid #fffbe7;
  max-width: 400px;
  margin: 30px auto;
  padding: 14px;
  border-radius: 12px;
}

.criado {
  background-color: #40dfef;
}

.atualizado {
  background-color: #fcba03;
}

.deletado {
background-color: red;  
}

#mensagem-container p {
  font-weight: bold;
}
</style>
