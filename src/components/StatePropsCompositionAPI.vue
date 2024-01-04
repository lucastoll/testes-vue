<script setup lang="ts">
import { ref } from 'vue';
import PropsTest from './PropsTest.vue';
    const count = ref(0);

    function incremented() {
        count.value++
    }
</script>

<template>
    <section>
        <h2>Variáveis de estado, props e emit</h2>
        <img :style="{ transform: `rotate(${count * 90}deg)` }" class="masterSword" src="../assets/images/masterSword.png" alt="Master sword">
        <PropsTest :count="count" @incremented="incremented"></PropsTest>
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
</style>