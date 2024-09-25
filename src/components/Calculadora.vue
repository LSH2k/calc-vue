<script setup>
import { reactive } from 'vue';

const estado = reactive({
    numA: '',
    numB: '',
    operacaoAritmetica: 'soma',
    operacoes: {
        soma: (a, b) => a + b,
        sub: (a, b) => a - b,
        mult: (a, b) => a * b,
        div: (a, b) => (b !== 0 ? a / b : 'Não é possível dividir por zero')
    },
    resultado: 0,
});

const calcRes = () => {
    const { numA, numB, operacaoAritmetica} = estado
    estado.resultado =  estado.operacoes[estado.operacaoAritmetica](Number(numA), Number(numB))
}

</script>

<template>
    <div class="container">
        <h1 class="mb-3 mt-5">Calculadora Aritmética</h1>
        <div class="row flex-nowrap">
            <div class="col-3">
                <input v-model="estado.numA" @input="calcRes" class="form-control" type="number">
            </div>
            <div class="col-1 w-auto">
                <select v-model="estado.operacaoAritmetica" @change="calcRes" class="form-control">
                    <option value="soma">➕</option>
                    <option value="sub">➖</option>
                    <option value="mult">✖️</option>
                    <option value="div">➗</option>
                </select>
            </div>
            <div class="col-3">
                <input v-model="estado.numB" @input="calcRes" class="form-control" type="number">
            </div>
            <div class="col-1 w-auto">
                <p>🟰</p>
            </div>
            <div class="col-4 me-2 rounded-3 text-center">
                {{ estado.resultado }}
            </div>
        </div>
    </div>
</template>

<style scoped>

.container {
    margin-top: 20px;
    background-color: #e4e4e4;

    p {
        line-height: 2.3;
    }

    .col-4 {
        background-color: white;
        max-height: 40px;
        line-height: 2.3;
        overflow: auto;
        flex: 1 1 auto;
    }

    .col-4::-webkit-scrollbar {
        display: none;
    }
}

</style>