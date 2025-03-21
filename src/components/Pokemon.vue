<script setup>
import { ref, onMounted, defineProps, computed} from 'vue'
import {RouterLink, useRouter} from 'vue-router'

const pokeList = defineProps({
        poke : Object
})
const router = useRouter()
function toDetail() {
    router.push({ path: `/${pokeList.poke.id}`, params: { id: pokeList.poke.id } })
}
const loadingPikachu = ref('https://scontent.fdad3-5.fna.fbcdn.net/v/t1.15752-9/476482524_1189551102797958_8162686971541914476_n.png?_nc_cat=107&ccb=1-7&_nc_sid=9f807c&_nc_eui2=AeHLr3FSkEmFXnhBQye0-YWeAnP6AeW2-D0Cc_oB5bb4PQfvq8_J10xHrWdWTeDuuspfZr2eRYi4GYD1V_oEIaBy&_nc_ohc=Vrjr1YqFp00Q7kNvgEr4q76&_nc_oc=AdjSFCjEktDPH7Fh6h4usOUAjSaSXKnNZNyqC1GVLhVALEAOJrdVDMHCGvITKGm-osQ&_nc_zt=23&_nc_ht=scontent.fdad3-5.fna&oh=03_Q7cD1gEsdauNfQhFcwfbFNnz3Y2jsv-vXqcLJlrzei1eRwfmPg&oe=67E76E71')
const imgSrc = computed(() => {
    return pokeList.poke.img || loadingPikachu
})

</script>
<template>
    <div class="card" @click="toDetail">
        <span v-if="poke.id">#{{ pokeList.poke.id }}</span>
        <img :src="imgSrc" alt="">
        <h3>{{ pokeList.poke.name }}</h3>
        <div class="element">
            <p v-for="type in pokeList.poke.types" :key="type" :class="type">{{ type }}</p>
        </div>
    </div>
</template>
<style scoped>
.card {
    background-color: white;
    padding: 10px;
    margin: 9px;
    height: 350px;
    width: 100%;
    font-size: 20px;
    text-align: center;
    border-radius: 20px;
    /* box-shadow: 0 0 20px rgba(0, 0, 0, 0.1); */
    box-shadow: #0000001a 0 4px 12px;
    cursor: pointer;
    transition: all ease 0.3s;
}
.card:hover{
    box-shadow: #0000002e 2px 15px 15px;
}
.card img{
    width: 100%;
}
#container2 .card p{
    display: inline-block;
    border-radius: 10px;
    padding: 8px 7px;
    font-size: 15px;
    margin: 0;
}
#container2 .card h3{
    margin: 0 5px;
}
.card{
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    gap: 10px;
    text-decoration: none;
    color: rgb(41, 36, 36);
}
.card .element{
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    cursor: pointer;
    gap: 10px;
}
.card .description {
    width: 180.8px;
    height: 180.8px;
    display: none;
    justify-content: center;
    align-items: center;
    border-top-left-radius: 10%;
    border-top-right-radius: 10%;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    border: solid 1px #5c565665;
    pointer-events: auto;
}
.grass{
    background-color: rgb(33, 218, 33);
}
.poison{
    background-color: rgb(168, 10, 168);
}
.fire{
    background-color: rgb(246, 66, 66);
}
.flying{
    background-color: rgba(146, 13, 169, 0.679);
}
.water{
    background-color: rgba(7, 7, 235, 0.525);
}
.bug{
    background-color: rgba(14, 228, 82, 0.616);
}
.normal{
    background-color: rgba(145, 145, 145, 0.616);
}
.rock{
    background-color: rgba(145, 145, 145, 0.616);
}
.electric{
    background-color: rgba(255, 255, 0, 0.616);
}
.dragon{
    background-color: rgba(146, 13, 169, 0.679);
}
.psychic{
    background-color: rgba(255, 0, 0, 0.616);
}
.fairy{
    background-color: rgba(189, 5, 147, 0.616);
}
.ground{
    background-color: rgba(62, 8, 8, 0.616);
}
.ghost{
    background-color: rgba(0, 0, 0, 0.616);
}
.fighting{
    background-color: rgba(176, 18, 18, 0.616);
}
.ice{
    /* //background color phải phù hợp với thuộc tính */
    background-color: rgba(12, 134, 221, 0.616);
}
.dark{
    background-color: rgba(1, 1, 1, 0.647);
}
.steel{
    background-color: rgba(145, 145, 145, 0.616);
}
</style>