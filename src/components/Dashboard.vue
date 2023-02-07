<template>
  <Message :msg="msg" v-show="Object.keys(msg).length != 0" />

  <div id="burger-table" v-if="burgers">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>

    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>

        <div>
          <ul>
            <li v-for="(opcional, index) in burger.optionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </div>

        <div>
          <select
            name="status"
            class="status"
            @change="updateStatus($event, burger.id)"
          >
            <option>Selecione</option>
            <option
              v-for="item in status"
              :key="item.id"
              :selected="item.tipo === burger.status"
              :value="item.tipo"
            >
              {{ item.tipo }}
            </option>
          </select>

          <button class="delete-btn" @click="handleDelete(burger.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
  <div v-else id="burger-table">
    Sem Pedidos!
  </div>

</template>

<script>
import Message from "./Message.vue";

export default {
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: {},
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();
      this.burgers = data;
      //get status
      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.status = data;
    },
    async updateStatus(event, id) {
      const status = event.target.value;
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ status }),
      });
      const data = await req.json();

      // message
      this.msg = {
        mensagem: "Pedido atualizado com successo.",
        status: "Atualizado",
      };

      //remover mensagem
      setTimeout(() => {
        this.msg = {};
      }, 3000);
    },
    async handleDelete(id) {
      await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });
      this.getPedidos();

      // message
      this.msg = {
        mensagem: "Pedido deletado com successo.",
        status: "Deletado",
      };

      //remover mensagem
      setTimeout(() => {
        this.msg = {};
      }, 3000);
    },
  },
  mounted() {
    this.getPedidos();
  },
  components: { Message, Message },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}
#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}
#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}
#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}
select {
  padding: 12px 6px;
  margin-right: 12px;
}
.delete-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
