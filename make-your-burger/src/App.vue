<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
  data() {
    return {
      logo_src: "/img/logo.svg",
      app_name: "Logo do site",
    };
  },

  components: {
    Navbar,
    Footer,
  },
};
</script>

<style>
:root {
  --main-color: #030303;
  --highlight-color: #d5c06b;
}

* {
  box-sizing: border-box;
  font-family: "Helvetica";
  margin: 0;
  padding: 0;
}

.main-container {
  color: var(--main-color);
  min-height: 100vh;
  padding: 4%;
}

@media (max-width: 834px) {
  h1 {
    font-size: 1.6rem;
  }
}

@media (max-width: 414px) {
  h1 {
    margin-top: 3vh;
  }
}

@media (max-width: 240px) {
  h1 {
    font-size: 1.3rem;
  }
}
</style>
