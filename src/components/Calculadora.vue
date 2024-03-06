<script setup>
import { reactive } from "vue";

let estado = reactive({
    valorA: 0,
    valorB: 0,
    resultado: 0,
    operacao: 'adicao',
});

const mudarOperacao = (event) => {
    estado.operacao = event.target.value;
    calcular();
};

const gravarValorA = (event) => {
    estado.valorA = event.target.value;
    calcular();
};

const gravarValorB = (event) => {
    estado.valorB = event.target.value;
    calcular();
};

const calcular = () => {
    let resultado = 0;
    let { operacao, valorA, valorB } = estado;

    switch (operacao) {
        case 'divisao':
            resultado = parseInt(valorA) / parseInt(valorB);
            break;
        case 'multiplicacao':
            resultado = parseInt(valorA) * parseInt(valorB);
            break;
        case 'subtracao':
            resultado = parseInt(valorA) - parseInt(valorB);
            break;
        case 'adicao':
            resultado = parseInt(valorA) + parseInt(valorB);
            break;
            default:
                resultado = 0;
                break;
    }
    estado.resultado = resultado;
};
</script>

<template>
    <header class="p-5 mb-5 mt-5 bg-dark rounded-4">
        <h1 class="title">Calculadora Aritmética</h1>
    </header>

    <form>
        <div class="row p-5">
            <div class="col-md-3">
                <input @keyup="gravarValorA" type="number" placeholder="Digite um número" required class="form-control" />
            </div>
            <div class="col-md-3">
                <input @keyup="gravarValorB" type="number" placeholder="Digite um número" required class="form-control"/>
            </div>
            <div class="col-md-2">
                <input type="number" :value="estado.resultado" placeholder="0" class="form-control" />
            </div>
            <div class="operacao col-md-4">
                <select @change="mudarOperacao" class="form-control">
                    <option value="selecione">Selecione uma operação...</option>
                    <option value="divisao">Divisão</option>
                    <option value="multiplicacao">Multiplicação</option>
                    <option value="subtracao">Subtração</option>
                    <option value="adicao">Adição</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style scoped>
.title {
    color: #fff;
}

::-webkit-inner-spin-button {
    display: none;
}

input {
    border-color: #333;
}

select {
    border-color: #333;
}
</style>
