<template>
<div>
    <ul>
        <li v-for="producte in productes" :key="producte.name">
         {{ producte.name }} - {{ producte.price }}€
        <button @click="addCart(producte)">Add Cart</button>
        </li>
    </ul>
</div>
</template>

<script setup>
import { ref, provide, inject } from 'vue';
const productes = inject('productes');

const emit = defineEmits (['añadir-al-carrito']);


const addCart = (producte) => {
    emit('añadir-al-carrito',producte);
}

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
  