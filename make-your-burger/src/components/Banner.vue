<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Vidaloka&display=swap");

#main-banner {
  align-items: center;
  background-image: url("/img/burger.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: bottom;
  display: flex;
  height: 50vh;
  justify-content: flex-start;
}

#main-banner h1 {
  background-color: var(--main-color);
  color: #fff;
  font-family: "Vidaloka", serif;
  font-size: 3.3rem;
  letter-spacing: 2px;
  margin-bottom: 4vh;
  margin-left: 10vw;
  padding: 20px 40px;
}

@media (max-width: 1440px) {
  #main-banner h1 {
    margin-left: 0;
  }
}

@media (max-width: 1280px) {
  #main-banner {
    background-position: 0 -300px;
    height: 43vh;
  }
}

@media (max-width: 1024px) {
  #main-banner {
    background-position: bottom;
    height: 340px;
  }

  #main-banner h1 {
    font-size: 2.9rem;
    margin-bottom: 60px;
    padding: 10px 20px;
  }
}

@media (max-width: 834px) {
  #main-banner {
    height: 300px;
  }

  #main-banner h1 {
    font-size: 2.5rem;
    margin-bottom: 60px;
    padding: 10px 20px;
  }
}

@media (max-width: 800px) {
  #main-banner h1 {
    padding: 10px;
  }
}

@media (max-width: 800px) {
  #main-banner h1 {
    font-size: 2.4rem;
  }
}

@media (max-width: 688px) {
  #main-banner {
    height: 250px;
  }

  #main-banner h1 {
    font-size: 2.2rem;
    padding: 7px;
  }

  @media (max-width: 600px) {
    #main-banner {
      height: 200px;
    }

    #main-banner h1 {
      font-size: 1.95rem;
      padding: 7px;
    }
  }
}

@media (max-width: 414px) {
  #main-banner {
    display: none;
  }
}
</style>
