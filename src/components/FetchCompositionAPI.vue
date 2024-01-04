<script setup lang="ts">
import { ref, watchEffect } from 'vue'

interface ApiResponse {
    count: number
    data: {
        id: number
        name: string
        released_date: string
    }[]
}

const games = ref<ApiResponse>({ data: [], count: 0 })
const gamesCount = ref<number>(0)
const error = ref<string>('')
const showFetchMoreButton = ref<boolean>(true)

watchEffect(async () => {
    const url = 'https://zelda.fanapis.com/api/games?name=%20&limit=10'
    games.value = await (await fetch(url)).json()
    gamesCount.value = games.value.count

    games.value.data.sort((a, b) => {
        const dateA = Number(a.released_date.split(',')[1])
        const dateB = Number(b.released_date.split(',')[1])
        return dateA - dateB
    })
})

async function fetchMoreGames() {
    const url = `https://zelda.fanapis.com/api/games?name=%20&limit=1&page=${gamesCount.value}`
    const response = await fetch(url)
    if (!response.ok) {
        console.error(`Erro na requisição: ${response.status}`)
        error.value = 'Houve um erro, tente novamente ' + response.status
    } else {
        const newData = await response.json()
        // if the response doesnt find any more games, the fetch button goes away
        if (newData.count === 0) {
            console.log('chegou')
            showFetchMoreButton.value = false
            console.log(showFetchMoreButton)
        } else {
            games.value.data.push(newData.data[0])

            games.value.data.sort((a, b) => {
                let dateA = Number(a.released_date.split(',')[1])
                let dateB = Number(b.released_date.split(',')[1])

                // Special treatment for zelda adventure game that doesnt contain month and day on the released date
                if (isNaN(dateA)) {
                    dateA = Number(a.released_date)
                }
                if (isNaN(dateB)) {
                    dateB = Number(b.released_date)
                }

                console.log(dateA, dateB)

                return dateA - dateB
            })

            console.log(newData)
            gamesCount.value++
        }
    }
}
</script>

<template>
    <section>
        <h2>API Requests e List Rendering</h2>
        <p>Jogos da franquia zelda vindos de uma api</p>
        <p v-if="error != ''">{{ error }}</p>
        <ul v-if="games.data.length > 0">
            <li v-for="game in games.data" :key="game.id">
                {{ game.name }} -
                {{
                    game.released_date.split(',')[1]
                        ? game.released_date.split(',')[1]
                        : game.released_date
                }}
            </li>
        </ul>
        <div v-else>Carregando...</div>
        <button v-if="showFetchMoreButton == true" @click="fetchMoreGames">
            Buscar mais jogos
        </button>
    </section>
</template>

<style scoped>
section {
    background: #4ed8a4;
    gap: 16px;
}
h2 {
    font-size: 24px;
    color: black;
}
p {
    color: black;
}
li {
    color: black;
    border: 1px solid black;
    padding: 4px;
}
button {
    background: transparent;
    padding: 16px;
    color: black;
    border: 1px solid black;
    font-size: 18px;
}
</style>
