<template>
  <nav>
    <router-link to="/">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>

    <div>
      <router-link to="/">Home</router-link>
      <router-link to="/pedidos">Pedidos</router-link>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
nav {
  align-items: center;
  background-color: var(--main-color);
  display: flex;
  justify-content: space-between;
  height: 14vh;
}

nav a {
  color: #fff;
  font-size: 1.5rem;
  margin-right: 4vw;
  padding-right: 10px;
  text-decoration: none;
  transition: 0.5s;
}

nav a:hover {
  color: var(--highlight-color);
}

#logo {
  margin-left: 4vw;
  width: 70px;
}

@media (max-width: 1024px) {
  nav {
    height: 100px;
  }
}

@media (max-width: 834px) {
  #logo {
    width: 60px;
  }
}

@media (max-width: 688px) {
  #logo {
    width: 50px;
  }
}

@media (max-width: 414px) {
  nav {
    display: block;
    text-align: center;
    height: 150px;
  }

  div {
    margin-top: 1vh;
  }

  a {
    display: block;
    margin-bottom: 1vh;
  }

  #logo {
    margin-left: 0;
    margin-top: 1vh;
  }
}

@media (max-width: 240px) {
  nav {
    height: 130px;
  }

  nav a {
    font-size: 1.3rem;
  }
}
</style>
