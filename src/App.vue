<script setup>
import { onMounted, ref } from 'vue';
import Footer from './components/Footer.vue';
import Header from './components/Header.vue';
import Guitarra from './components/Guitarra.vue';
import {db} from './data/guitarras.js'

const guitarras = ref([])

onMounted( ()=>{
    guitarras.value = db
});



</script>

<template>

    <Header/>


    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>  

        <Guitarra
            v-for="guitarra in guitarras"
            :key="guitarra.id"
            :guitarra="guitarra"
        />
            
    </main>

    <Footer/>
    
</template>


