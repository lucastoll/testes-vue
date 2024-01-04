<script setup lang="ts">
const props = defineProps({
    count: Number
})
const emits = defineEmits(['incremented'])

function increment() {
    emits('incremented', props.count)
}
</script>

<template>
    <button @click="increment">Girar master sword</button>
    <p>A master sword ja foi girada: {{ count }} vezes</p>
</template>

<style scoped>
button {
    width: 200px;
    height: 40px;
    background: #1e68a7;
    border: 2px solid white;
    margin: 32px 0;
}
</style>
