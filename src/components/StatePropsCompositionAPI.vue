<script setup lang="ts">
import { ref } from 'vue';
    const count = ref(0);

    function increment() {
        count.value++
    }
</script>

<template>
    <section>
        <h2>Variáveis de estado</h2>
        <img :style="{ transform: `rotate(${count * 90}deg)` }" class="masterSword" src="../assets/images/masterSword.png" alt="Master sword">
        <button @click="increment">Girar master sword</button>
        <p>A master sword ja foi girada: {{ count }} vezes</p>
    </section>
</template>

<style scoped>
    section{
        width: 100%;
        padding: 16px;
        background: #1E68A7;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    h2{
        font-size: 24px;
    }
    .masterSword{
        margin-top: 32px;
        height: 200px;
        transition: 1s transform ease-in-out;
    }

    button{
        width: 200px;
        height: 40px;
        background: #1E68A7;
        border: 2px solid white;
        margin: 32px 0;
    }
</style>