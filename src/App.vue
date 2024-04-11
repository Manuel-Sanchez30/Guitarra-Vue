<script setup>
import { onMounted, ref } from 'vue';
import Footer from './components/Footer.vue';
import Header from './components/Header.vue';
import Guitarra from './components/Guitarra.vue';
import {db} from './data/guitarras.js'

const guitarras = ref([])
const carrito = ref([])

onMounted( ()=>{
    guitarras.value = db
});

const agregarCarrito = (guitarra)=>{

    guitarra.cantidad = 1
    carrito.value.push(guitarra)
};

console.log(carrito);


</script>

<template>

    <Header
    
        :carrito="carrito"
    />


    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>  

        <Guitarra
            v-for="guitarra in guitarras"
            :key="guitarra.id"
            :guitarra="guitarra"
            @agregar-carrito="agregarCarrito"
        />
            
    </main>

    <Footer/>
    
</template>


