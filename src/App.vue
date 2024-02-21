<script setup>
import { isBreakOrContinueStatement, isCallSignatureDeclaration } from 'typescript';
import { reactive } from 'vue';

  const estado = reactive({
    valorA: 0,
    valorB: 0, 
    resultado: 0,
    operacao: 'adicao',
  })

  const mudarOperacao = (event) => {
    estado.operacao = event.target.value;
    calcular();
  }

  const gravaValorA = (event) => {
    estado.valorA = event.target.value;
    calcular();
  }

  const gravaValorB = (event) => {
    estado.valorB = event.target.value;
    calcular();
  }

  const calcular = () => {
    let resultado = 0; 
    let { operacao, valorA, valorB} = estado;

    switch(operacao) {
      case 'adicao':
        resultado = parseInt(valorA) + parseInt(valorB);
        break;
      case 'subtracao':
        resultado = parseInt(valorA) - parseInt(valorB);
        break;
      case 'multiplicacao':
        resultado = parseInt(valorA) * parseInt(valorB);
        break;
      case 'divisao':
        resultado = parseInt(valorA) / parseInt(valorB);
        break;
      default:
        resultado = 0;
        break;
    }
    estado.resultado = resultado;
  }


  
</script>

<template>
    <div class="container conta__container">
      <div class="operacao">
        <select @change="mudarOperacao">
          <option value="adicao">+</option>
          <option value="subtracao">-</option>
          <option value="multiplicacao">x</option>
          <option value="divisao">÷</option>
        </select>
      </div>
      <div class="numeros">
        <input @keyup="gravaValorA" type="number" placeholder="Digite o primeiro valor">
        <input @keyup="gravaValorB" type="number" placeholder="Digite o segundo valor">
      </div>
    </div>
    <div class="resultado">
      <p>Resultado:</p>
      <input type="text" :value="estado.resultado" disabled/>
    </div>
</template>

<style scoped>
  *{
    font-family: sans-serif;
    font-size: 14px;
    margin: 0 auto;
  }

  .container{
    margin-top: 16px;
    margin-bottom: 16px;
    width: 250px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    align-items: center;
  }

  .numeros input{
    margin-bottom: 8px;
  }

  input{
    padding: 8px;
  }

  .resultado{
    width: 125px;
  }

  .resultado input{
    border: 2px solid #5f45d4;
    border-radius: 3px;
    color: #332a5e;
    font-weight: bold;
  }

  select{
    padding: 8px;
    margin-right: 8px;
    background-color: #5f45d4;
    border: 1px solid #5f45d4;
    border-radius: 3px;
    color: white;
  }


</style>
