<template>
  <div class="Xat"></div>

    <h1>{{ titulo }}</h1>
    <input v-model="titulo">
    <button @click="" placeholder="Escribe el titulo">Enviar</button>
    
    <Producte :productes="productes" @añadir-al-carrito="addCart"/>
    <!-- Fill Producte / Pasem productes / @ (Funcio Fill al clicar envia el emit)-->
 
</template>

<script setup>
import { ref, provide, inject } from 'vue';
import Producte from './components/Producte.vue'
import List from './components/List.vue'
import Divisa from './components/Divisa.vue'

provide('productes',productes);
provide('cart',cart);


const titulo = ref('');

const productes = ref([
{ name: "Hamburger 🍔.", price: 5 },
{ name: "Cheeseburger 🧀", price: 6 },
{ name: "Impossible Burger 🥕", price: 7 },
{ name: "Fries 🍟", price: 2 }
]);


const addCart = (producte) => {
  cart.value.push(producte);
  alert(`Añadido al carrito: ${producte.name}`);
};

const cart = [

];

</script>

<!-- Producte.vue -->
<template>
  <div>
    <h2>Productos</h2>
    <ul>
      <li v-for="producte in productes" :key="producte.name">
        {{ producte.name }} - {{ producte.price }}€
        <button @click="addProductToCart(producte)">Add Cart</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { inject } from 'vue';

// Inyectamos `productes` y `addCart` proporcionados desde `App.vue`
const productes = inject('productes');
const addCart = inject('addCart');

// Función para añadir un producto al carrito usando `addCart` inyectado
const addProductToCart = (producte) => {
  addCart(producte);
};
</script>

<style scoped>
/* Estilos */
</style>
