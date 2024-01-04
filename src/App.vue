<script setup lang="ts">
import FetchCompositionAPIVue from './components/FetchCompositionAPI.vue'
import HeaderOptionsAPI from './components/HeaderOptionsAPI.vue'
import StatePropsCompositionAPI from './components/StatePropsCompositionAPI.vue'
</script>

<template>
    <HeaderOptionsAPI></HeaderOptionsAPI>
    <main>
        <StatePropsCompositionAPI></StatePropsCompositionAPI>
        <FetchCompositionAPIVue></FetchCompositionAPIVue>
    </main>
</template>
