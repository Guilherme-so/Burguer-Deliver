<template>
  <div>
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Nome do cliente:</label>
          <input
            type="text"
            id="nome"
            name="nome"
            placeholder="Digite seu nome"
            v-model="nome"
          />
        </div>
        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Select seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a sua carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Select sua carne:</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>

        <div id="optinais-container" class="input-container">
          <label id="optionais-title" for="opcionais"
            >Selecione os opcionais:</label
          >
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisData"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              :value="opcional.tipo"
              v-model="opcionais"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu burger" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisData: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const request = await fetch("http://localhost:3000/ingredientes");
      const data = await request.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisData = data.opcionais;

      console.log(this.paes);
      console.log(this.carnes);
      console.log(this.opcionaisData);
    },
    async createBurger(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        optionais: Array.from(this.opcionais),
        status: "Solicitado",
      };

      const request = await fetch("http://localhost:3000/burgers",{
        method:"POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
      })

      const res = await request.json()


      this.nome = "";
      this.pao = "";
      this.carne = "";
      this.opcionais = [];
    },
  },
  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  padding: 5px 10px;
  color: #222;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#optinais-container {
  flex-direction: row;
  flex-wrap: wrap;
}

.optionais-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  margin-left: 5px;
  font-weight: bold;
}

.submit-btn {
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

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
