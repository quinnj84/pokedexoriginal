<template>
    <div class="flex flex-col space-y-6">
        <h1 class="text-6xl text-purple-600 font-semibold">
            {{ pokemonDetails?.name }} 
        </h1>
        <img :src="image" :alt="pokemonDetails?.name" class="w-full h-full rounded-lg" />
        <div>
            <div class="flex items-center justify-between">
                <span class="attributes"> Primary Type :</span>
                <span><strong> {{ pokemonDetails?.type1 }} </strong></span>
            </div>
    
            <div class="flex items-center justify-between" v-if="pokemonDetails?.type2">
                <span class="attributes"> Secondary Type :</span>
                <span><strong> {{ pokemonDetails?.type2 }} </strong></span>
            </div>    
        </div>
        
        
        <div>
            <div class="flex items-center justify-between">
                <span class="attributes"> Weight :</span>
                <span><strong> {{ pokemonDetails?.stats?.weight_kg }} Kg </strong></span>
            </div>
            
            <div class="flex items-center justify-between">
                <span class ="attributes"> Height :</span>
                <span><strong>  {{ pokemonDetails?.stats?.height_m }} m </strong></span>
            </div>
            
            <div class="flex items-center justify-between">
                <span class="attributes"> HP :</span>
                <span><strong> {{ pokemonDetails?.stats?.hp }} pts </strong></span>
            </div>
            
            <div class="flex items-center justify-between">
                <span class ="attributes"> Attack :</span>
                <span><strong> {{ pokemonDetails?.stats?.attack }} pts </strong></span>
            </div>

            <div class="flex items-center justify-between">
                <span class="attributes"> Speed :</span>
                <span><strong> {{ pokemonDetails?.stats?.speed }} pts</strong></span>
            </div>
            
            <div class="flex items-center justify-between">
                <span class ="attributes"> Defense :</span>
                <span><strong> {{ pokemonDetails?.stats?.defense }} pts </strong></span>
            </div>
        </div>
    </div>
<br>
<form>
    <input class="button" type="button" value="Back" onclick="history.back()">
</form>
</template>

<script setup>
import { useRoute } from 'vue-router';
import pokemons from "@/assets/sampledataset.json";
import { onMounted, ref } from "vue";
import client from "@/assets/apiclient.js";
import axios from "axios";

const route = useRoute();

//passing name as a route parameter. check router/index.js for more details
const pokemonDetails = ref({});

const image = ref("")

onMounted(()=>{
    // pokemonDetails.value = pokemons.filter(
    //     (item) => item.name.toLowerCase() == route.params.name.toLowerCase()
    //     )[0];

    client
    .get(`/pokemon/${route.params.name}`)
    .then((res) => {
        console.log("response received", res.data);
        pokemonDetails.value = res.data;

    axios
        .get(
        `http://pokeapi.co/api/v2/pokemon/${pokemonDetails.value.name.toLowerCase()}`
        )
        .then((data) => {
            image.value = 
                data.data.sprites.other['official-artwork'].front_default
        });
    })
    
    .catch((errors) => {
        console.log("error", errors);
    })
});
</script>