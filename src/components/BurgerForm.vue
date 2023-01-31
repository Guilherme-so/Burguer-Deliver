<template>
  <div>
    <div>
      <form id="burger-form">
        <div class="input-container">
          <label for="nome">Nome do cliente:</label>
          <input
            type="text"
            id="nome"
            name="nome"
            placeholder="Digite seu nome"
          />
        </div>
        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao">
            <option value="">Select seu pão</option>
            <option value="integral">Integral</option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a sua carne:</label>
          <select name="carne" id="carne">
            <option value="">Select sua carne:</option>
            <option value="maminha">Maminha</option>
          </select>
        </div>

        <div id='optinais-container' class="input-container">
          <label id="optionais-title" for="opcionais">Selecione os opcionais:</label>
          <div class="checkbox-container">
            <input type="checkbox" name="opcionais" value="salame">
            <span>Salame</span>
          </div>
        </div>

        <div class="input-container">
            <input type="submit" class="submit-btn" value="Criar meu burger">
        </div>
      </form>
    </div>
  </div>
</template>


<style scoped>
#burger-form{
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    padding: 5px 10px;
    color: #222;
    border-left: 4px solid #FCBA03;
}

input, select {
    padding: 5px 10px;
    width: 300px;
}

#optinais-container{
    flex-direction: row;
    flex-wrap: wrap;
}

.optionais-title{
    width: 100%;
}

.checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
} 

.checkbox-container span,
.checkbox-container input {
    width: auto;

}

.checkbox-container span{
    margin-left: 5px;
    font-weight: bold;
}

.submit-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover{
    background-color: transparent;
    color: #222;
}

</style>