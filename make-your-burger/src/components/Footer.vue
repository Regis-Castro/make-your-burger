<template>
  <footer>
    <p>Make your burger &copy; 2023</p>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
footer {
  align-items: center;
  background-color: var(--main-color);
  bottom: 0;
  color: var(--highlight-color);
  display: flex;
  height: 14vh;
  justify-content: center;
}

@media (max-width: 1024px) {
  footer {
    height: 10vh;
  }
}

@media (max-width: 834px) {
  footer {
    height: 8vh;
  }
}
</style>
