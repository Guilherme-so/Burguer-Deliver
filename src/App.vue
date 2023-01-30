<script setup>
import { RouterView } from "vue-router";
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <Navbar :logo="logo" :v-bind="alt" />
  <RouterView />
  <Footer />
</template>

<script>
export default {
  data(){
    return {
      logo: "/img/logo.png",
      alt: "Burguer Deliver"
    }
  }
}
</script>

<style>
* {
  font-family: helvetica;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 42px;
  color: #222;
  margin-bottom: 30px;
}

</style>
