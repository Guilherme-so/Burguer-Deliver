<template>
  <footer id="footer">
    <p>Peça ja seu Burguer &copy; {{ new Date().getFullYear() }}</p>
  </footer>
</template>

<style scoped>
#footer {
    height: 200px;
    background-color: #222;
    color: #FCBA03;
    display: flex;
    justify-content: center;
    align-items: center;
    border-top: 4px solid #FCBA03;
    bottom: 0;
    width: 100%;
}

</style>
