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

    const existe = carrito.value.findIndex( producto => producto.id === guitarra.id )
    if( existe >=0 ){
        carrito.value[existe].cantidad ++
    }else{
        guitarra.cantidad = 1
        carrito.value.push(guitarra)
    }
};

const decrementarCantidad = (id)=>{

    const index = carrito.value.findIndex( producto => producto.id === id )
    if( carrito.value[index].cantidad <=1 ) return
    carrito.value[index].cantidad--
};

const aumentarCantidad = (id)=>{

    const existe = carrito.value.findIndex( producto => producto.id === id )
    carrito.value[existe].cantidad++
};

const eliminarProducto = (id)=>{
    carrito.value = carrito.value.filter( product => product.id !== id )
};

const vaciarCarrito = ()=>{
    carrito.value = []
};


</script>

<template>

    <Header
    
        :carrito="carrito"
        @disminuir-carrito="decrementarCantidad"
        @aumentar-cantidad="aumentarCantidad"
        @eliminar-producto="eliminarProducto"
        @vaciar-carrito="vaciarCarrito"
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


