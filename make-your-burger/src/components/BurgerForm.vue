<template>
  <h1>Monte o seu hambúrguer</h1>
  <Message :msg="msg" v-show="msg" />

  <div>
    <form id="burger-form" @submit.prevent="createBurger">
      <div class="input-container">
        <label for="nome">Nome do cliente:</label>
        <input
          type="text"
          id="nome"
          name="nome"
          v-model="nome"
          placeholder="Digite seu nome"
          required
        />
      </div>

      <div class="input-container">
        <label for="pao">Escolha o pão:</label>
        <select name="pao" id="pao" v-model="pao" required>
          <option value="">Selecione o seu pão</option>
          <option v-for="pao in paes" :value="pao.tipo" :key="pao.id">
            {{ pao.tipo }}
          </option>
        </select>
      </div>

      <div class="input-container">
        <label for="carne">Escolha a carne:</label>
        <select name="carne" id="carne" v-model="carne" required>
          <option value="">Selecione o tipo de carne</option>
          <option v-for="carne in carnes" :value="carne.tipo" :key="carne.id">
            {{ carne.tipo }}
          </option>
        </select>
      </div>

      <div id="opcionais-container" class="input-container">
        <label id="opcionais-title">Selecione os opcionais:</label>
        <div
          v-for="opcional in opcionaisdata"
          class="checkbox-container"
          id="opcionais"
          :key="opcional.id"
        >
          <label :for="opcional.id">
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
              :id="opcional.id"
            />
            <span>{{ opcional.tipo }}</span>
          </label>
        </div>
      </div>

      <div class="input-container">
        <input type="submit" class="submit-btn" value="Criar meu hambúrguer!" />
      </div>
    </form>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "BurgerForm",
  components: {
    Message,
  },

  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,

      nome: "",
      pao: "",
      carne: "",
      opcionais: [],
      msg: null,
    };
  },

  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },

    async createBurger() {
      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-type": "application/json" },
        body: dataJson
      });

      const res = await req.json(); 

      this.msg = `Pedido realizado com sucesso`;
      setTimeout(() => (this.msg = ""), 3000);

  
      this.nome = "",
      this.pao = "",
      this.carne = "",
      this.opcionais = [];
    },
  },

  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
h1,
p {
  text-align: center;
}

#burger-form {
  margin: 8vh auto;
  max-width: 30vw;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 4vh;
}

.input-container > label {
  color: var(--main-color);
  border-left: 4px solid var(--highlight-color);
  font-weight: bold;
  margin-bottom: 0.5vh;
  padding: 5px 10px;
}

.checkbox-container label > input {
  cursor: pointer;
}

input,
select {
  padding: 10px;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
  width: 53%;
}

#opcionais-title {
  margin-bottom: 1vh;
}

.checkbox-container {
  align-items: flex-start;
  display: flex;
  margin-bottom: 2vh;
  width: 50%;
}

.checkbox-container span {
  cursor: pointer;
  margin-left: 0.5vw;
}

.submit-btn {
  background-color: var(--main-color);
  border: none;
  color: var(--highlight-color);
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
  margin: 0 auto;
  padding: 10px;
  transition: 0.5s;
  width: 30vw;
}

.submit-btn:hover {
  background-color: var(--highlight-color);
  color: var(--main-color);
}

@media (max-width: 1440px) {
  #burger-form {
    max-width: 40vw;
  }

  #opcionais-container {
    width: 28vw;
  }

  .submit-btn {
    width: 40vw;
  }
}

@media (max-width: 834px) {
  #burger-form {
    max-width: 50vw;
  }
}

@media (max-width: 1024px) {
  #burger-form {
    margin: 4vh auto;
  }
  .input-container {
    margin-bottom: 2vh;
  }

  #opcionais-container {
    width: 40vw;
  }
}

@media (max-width: 834px) {
  h1 {
    font-size: 1.8rem;
  }
  .submit-btn {
    width: 50vw;
  }

  .checkbox-container {
    margin-bottom: 1.3vh;
  }

  #opcionais-container {
    width: 48vw;
  }
}

@media (max-width: 800px) {
  h1 {
    font-size: 1.7rem;
  }
}

@media (max-width: 768px) {
  h1 {
    font-size: 1.5rem;
  }
}

@media (max-width: 688px) {
  #opcionais-container {
    width: 59vw;
  }
}

@media (max-width: 414px) {
  h1 {
    font-size: 1.3rem;
  }

  #burger-form {
    max-width: 80vw;
  }

  #opcionais-container {
    width: 80vw;
  }

  .submit-btn {
    margin-top: 2.5vh;
    width: 80vw;
  }
}
</style>
