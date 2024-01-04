<script setup lang="ts">
import { ref, watchEffect } from 'vue';

interface ApiResponse {
  count: number;
  data: {
    id: number;
    name: string;
    released_date: string;
  }[];
}

const games = ref<ApiResponse>({ data: [], count: 0 });
const gamesCount = ref<number>(0);

watchEffect(async () => {
  const url = "https://zelda.fanapis.com/api/games?limit=10";
  games.value = await (await fetch(url)).json();
  gamesCount.value = games.value.count;
  
  games.value.data.sort((a, b) => {
    const dateA = Number(a.released_date.split(',')[1]);
    const dateB = Number(b.released_date.split(',')[1]);
    return dateA - dateB;
  });

});

async function fetchMoreGames(){
  const url = `https://zelda.fanapis.com/api/games?limit=1&page=${gamesCount.value}`;
  const response = await fetch(url);
  const newData = await response.json();

    // Concatena os novos resultados à lista existente
    games.value.data.push(newData.data[0]);

    games.value.data.sort((a, b) => {
    const dateA = Number(a.released_date.split(',')[0]);
    const dateB = Number(b.released_date.split(',')[0]);
    return dateA - dateB;
  });

    console.log(games.value)
    gamesCount.value++;
}


</script>

<template>
    <section>
        <h2>
            API Requests e List Rendering
        </h2>
        <p>
            Os 10 primeiros jogos do zelda vindos de uma api
        </p>
        <ul v-if="games.data.length > 0">
            <li v-for="game in games.data" :key="game.id">
                {{ game.name }} - {{ game.released_date.split(',')[1] }}
            </li>
        </ul>
        <div v-else>
        Carregando...
        </div>
        <button @click="fetchMoreGames">
            Buscar mais jogos
        </button>
    </section>
</template>

<style scoped>
    section{
        background: #4ED8A4;
        gap: 16px;
    }
    h2{
        font-size: 24px;
        color: black;
    }
    p{
        color: black;
    }
    li{
        color: black;
        border: 1px solid black;
        padding: 4px;
    }
    button{
        background: transparent;
        padding: 16px;
        color: black;
        border: 1px solid black;
        font-size: 18px;
    }
</style>
