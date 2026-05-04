<script setup>
import { reactive } from 'vue';

    const estado = reactive({
        operation: {
            field1: 0,
            field2: 0,
            operator: "+"
        },
        result: 0,
        showResult: false 
    })

    const calculo = () => {
        const { field1, operator, field2 } = estado.operation
        estado.showResult = true

        switch(operator) {
            case '+':
                return field1 + field2
            case '-':
                return field1 - field2
            case 'x':
                return field1 * field2
            case '/':
                return field1 / field2
        }
    }

</script>

<template>
    <div class="app pt-5">
       <div class="container">
         <form action="">
        <input @keyup="evento => estado.operation.field1 = evento.target.value" v-model="estado.operation.field1" type="number" class="ms-4">
        <div class="operator">
            <select v-model="estado.operation.operator" name="" id="">
                <option value="+">+</option>
                <option value="-">-</option>
                <option value="x">x</option>
                <option value="/">/</option>
            </select>
        </div>
        <input @keyup="evento => estado.operation.field2 = evento.target.value" v-model="estado.operation.field2" type="number">
        <button type="button" @click="calculo()" @submit.prevent class="ms-4 p-1 ps-2">Calcular <i class="bi bi-plus-slash-minus ms-2"></i></button>
    </form>
       </div>
       <div class="container">
        <div v-if="estado.operation.field1 && estado.operation.field2 > 0" class="cardResult">
        <h4>Resultado</h4>
        <p v-if="estado.showResult" class="result">{{ calculo() }}</p>
       </div>
       </div>
    </div>
</template>

<style scoped>

    .app {
        background-color: #1b1b1b;
        width: 100%;
        min-height: 100vh;
        text-align: center;
    }

    .container {
        padding: 32px 0;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    form {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
    }

    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    input[type="number"] {
        background-color: #1b1b1b;
        border: 2px solid rgb(230, 132, 21);
        border-radius: 4px;
        color: #e6e3e3;
        font-size: 18px;
        text-align: center;
        outline: none;
        text-decoration: none;
        font-weight: 500;
        padding: 16px;
    }

    select {
        margin: 0 24px;
        background-color: #1b1b1b;
        color: rgb(190, 187, 181);
        font-size: 20px;
        display: flex;
        border: 2px solid rgb(230, 132, 21);
        appearance: none;
        -webkit-appearance: none;
        -moz-appearance: none;
        width: 36px;
        text-align: center;
        border-radius: 4px;
        font-weight: 700;
        cursor: pointer;

        &:hover {
            transform: scale(1.02);
        }
    }

    .operator {
        display: flex;
        align-items: center;
        height: 24px;
        justify-content: center;
    }

    button {
        color: #fff;
        background-color: #1b1b1b;
        font-weight: 600;
        font-size: 18px;
        border-radius: 4px;
        border: 2px solid rgb(230, 132, 21);
        display: flex;

        &:hover {
            transform: scale(1.02);
        }

        i {
            color: rgb(230, 132, 21);
        }
    }

    .result {
        color: #fff;
    }

    .cardResult {
        border: 2px solid rgb(230, 132, 21);
        color: #e6e3e3;
        margin: 0 auto;
        text-align: center;
        max-width: auto;
        display: block;
        text-align: center;
        justify-content: center;
        height: auto;
        padding: 8px;
        border-radius: 4px;

        p {
            font-size: 24px;
            font-weight: bold;
        }
    }

</style>