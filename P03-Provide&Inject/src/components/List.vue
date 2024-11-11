<template>
    <div>
      <h2>Carrito</h2>
      <ul>
        <li v-for="producto in cart" :key="producto.name">
          {{ producto.name }} - {{ calcularPrecio(producto.price) }}
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { inject } from 'vue';
  
  const cart = inject('cart');
  const calcularPrecio = inject('calcularPrecio');
  </script>
s  