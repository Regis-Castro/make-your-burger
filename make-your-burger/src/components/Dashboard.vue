<template>
  <Message :msg="msg" v-show="msg" />

  <table>
    <tr class="wrap">
      <th>#</th>
      <th>Cliente</th>
      <th>Pão</th>
      <th>Carne</th>
      <th>Opcionais</th>
      <th>Ações</th>
    </tr>
    <tr class="wrap" v-for="burger in burgers" :key="burger.id">
      <td>
        <b>{{ burger.id }})</b>
      </td>
      <td>{{ burger.nome }}</td>
      <td>{{ burger.pao }}</td>
      <td>{{ burger.carne }}</td>
      <td>
        <ul>
          <li v-for="(opcional, index) in burger.opcionais" :key="index">
            {{ opcional }}
          </li>
        </ul>
      </td>
      <td id="flex">
        <select name="status" @change="updateBurger($event, burger.id)">
          <option value="">Selecione</option>
          <option
            v-for="status in statuses"
            :value="status.tipo"
            :selected="burger.status == status.tipo"
            :key="status.id"
          >
            {{ status.tipo }}
          </option>
        </select>
        <button @click="deleteBurger(burger.id)">Cancelar</button>
      </td>
    </tr>
  </table>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "Dashboard",
  data() {
    return {
      burgers: null,
      burger_id: null,
      statuses: [],
      msg: null,
    };
  },

  components: {
    Message,
  },

  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();
      this.burgers = data;

      this.getStatus();
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/statuses");
      const data = await req.json();

      this.statuses = data;
    },

    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });

      const res = await req.json();

      this.msg = `Pedido nº${id} foi removido com sucesso!`;
      setTimeout(() => (this.msg = ""), 3000);

      this.getPedidos();
    },

    async updateBurger(event, id) {
      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option });
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      if (res.status != "") {
        this.msg = `O status do pedido nº${id} foi alterado para "${res.status}"`;
        setTimeout(() => (this.msg = ""), 3000);
      }
    },
  },

  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
table {
  border-spacing: 0 1rem;
  margin: 5vh auto;
  width: 70vw;
}

th {
  border-bottom: 3px solid #333;
  padding-bottom: 1vh;
}

tr td {
  border-bottom: 1px solid #ccc;
  padding-bottom: 4vh;
  text-align: center;
}

ul {
  list-style-position: inside;
  text-align: justify;
  padding-left: 5vw;
}

select {
  padding: 12px;
  width: 12vw;
}

button {
  background-color: var(--main-color);
  border: none;
  color: var(--highlight-color);
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
  margin-left: 1vw;
  padding: 10px;
  transition: 0.5s;
  width: 9vw;
}

button:hover {
  background-color: #cc0000;
  color: #fff;
}

.message-container {
  position: fixed;
  top: 280px;
  left: 42vw;
}

@media (max-width: 1440px) {
  .message-container {
    top: 182px;
    left: 35vw;
  }
}

@media (max-width: 1280px) {
  table {
    width: 92vw;
  }

  .message-container {
    padding: 6px;
    top: 140px;
  }
}

@media (max-width: 1024px) {
  .message-container {
    max-width: 50vw;
    top: 178px;
    left: 31vw;
  }
}

@media (max-width: 834px) {
  .message-container {
    max-width: 70vw;
    left: 25vw;
  }

  table {
    width: 60vw;
  }

  .wrap {
    display: flex;
    flex-direction: column;
  }

  th {
    margin-top: 2px;
    padding: 0;
    text-align: left;
  }

  tr {
    margin-bottom: 6vh;
  }

  tr td {
    padding: 0;
    text-align: left;
  }

  ul {
    list-style: outside;
  }

  select {
    padding: 9.5px;
  }

  button,
  select {
    width: auto;
  }
}

@media (max-width: 800px) {
  .message-container {
    top: 170px;
  }
}

@media (max-width: 768px) {
  table {
    width: 60vw;
  }
}

@media (max-width: 600px) {
  table {
    width: 60vw;
  }

  .message-container {
    top: 160px;
    left: 17vw;
    padding: 5px;
  }
}

@media (max-width: 414px) {
  table {
    width: 80vw;
  }

  .message-container {
    max-width: 100vw;
    left: 14px;
    top: 220px;
    right: 14px;
    padding: 0;
  }
}

@media (max-width: 412px) {
  .message-container {
    left: 20px;
    right: 0;
    left: 0;
  }
}

@media (max-width: 360px) {
  .message-container {
    top: 215px;
  }
}

@media (max-width: 240px) {
  .message-container {
    top: 186px;
  }
}
</style>
