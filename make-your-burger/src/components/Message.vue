<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  background-color: #cce5ff;
  border: 2px solid #b8daff;
  border-radius: 5px;
  color: #004085;
  max-width: 30vw;
  margin: 20px auto auto auto;
  padding: 10px;
  text-align: center;
}

@media (max-width: 1440px) {
  .message-container {
    max-width: 40vw;
  }
}

@media (max-width: 834px) {
  .message-container {
    max-width: 50vw;
  }
}

@media (max-width: 414px) {
  .message-container {
    max-width: 80vw;
  }
}
</style>
