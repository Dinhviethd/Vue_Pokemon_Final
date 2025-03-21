<script setup>
import { ref, onMounted } from 'vue'
import Pokemon from '../components/Pokemon.vue'

const isVisibleContainer = ref(false)
const isVisibleLoading = ref(true)
const pokeList = ref([])
const searchTerm = ref('')
const limit = ref(36)
const offset = ref(0)

async function fetchData() {
    const response = await fetch(`https://pokeapi.co/api/v2/pokemon?limit=${limit.value}&offset=${offset.value}`)
    const data = await response.json()
    const pokeDetail = []
    for (let i = 0; i < data.results.length; i++) {
        const item = data.results[i]
        const detailResponse = await fetch(item.url)
        const detailData = await detailResponse.json()
        pokeDetail.push({
            id: offset.value + i + 1,
            name: item.name.charAt(0).toUpperCase() + item.name.slice(1),
            url: item.url,
            img: detailData.sprites.front_default,
            types: detailData.types.map(type => type.type.name)
        })
    }
    pokeList.value = [...pokeList.value, ...pokeDetail]
    isVisibleContainer.value = true
    isVisibleLoading.value = false
}

function loadMore() {
    offset.value += limit.value
    limit.value *= 2
    fetchData()
}
const filteredPokemon = () => {
    return pokeList.value.filter(poke => poke.name.toLowerCase().includes(searchTerm.value.toLowerCase()))
}
onMounted(async () => {
    fetchData()
})

</script>

<template>
<body>
    <div v-if="isVisibleLoading" class="loading">Getting data from Pokédex...</div>
    <div v-if="isVisibleContainer" class="container">
        <div id="header">Pokemon API</div>
        <div id="container1">
            <input type="text" v-model="searchTerm" id="search" placeholder="Search some Pokemon...">
        </div>
        <div id="container2">
            <Pokemon v-for="poke in filteredPokemon()" :poke="poke" class="card"/>
        </div>
        <button class="loadMore" @click="loadMore">Load More</button>
    </div>
</body>
</template>

<style>
body{
    /* width: 90%; */
    margin: 0 100px;
    font-family: Arial, Helvetica, sans-serif;
    color: rgb(46, 44, 107);
}
.loadMore {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 20px auto;
    cursor: pointer;
    padding: 20px 25px;
    border: none;
    border-radius: 10px;
    font-size: 16px;
    color: #fff;
    background-color: #ff4d4f;
    transition: all 0.3s;
}
.loadMore:hover {
    background-color: #ff7875;
}
.loading {
    font-size: 24px;
    text-align: center;
    color: gray;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
#header{
    font-size: 50px;
    margin: 40px 0;
    text-align: center;
}

#container1{
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin: 40px 0;
    gap: 20px;
    width: 100%;
}
input{
    padding: 25px;
    width: 40%;
    border: 2px solid #ddd;
    border-radius: 40px;
    margin-top: 40px;
    font-size: 20px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

#container2{
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    justify-content: center;
    align-items: center;
    gap: 40px;
    width: 100%;
}

@media screen and (max-width: 1200px) {
    #container2{
        grid-template-columns: repeat(4, 1fr);
    }
}
@media screen and (max-width: 800px) {
    #container2{
        grid-template-columns: repeat(3, 1fr);
    }
}
@media screen and (max-width: 600px) {
    #container2{
        grid-template-columns: repeat(2, 1fr);
    }
}
</style>