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
}
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
  min-height: 72vh;
  padding: 4%;
}

@media (max-width: 1024px) {
  .main-container {
    min-height: 60vh;
  }
}

@media (max-width: 834px) {
  h1 {
    font-size: 1.6rem;
  }

  .main-container {
    min-height: 60.75vh;
  }
}

@media (max-width: 414px) {
  h1 {
    margin-top: 3vh;
  }

  .main-container {
    min-height: 75.3vh;
  }
}

@media (max-width: 240px) {
  h1 {
    font-size: 1.3rem;
  }
}
</style>
