<template>
  <div>
    <h2>Productos Disponibles</h2>
    <ul>
      <li v-for="producto in productos" :key="producto.name">
        {{ producto.name }} - {{ calcularPrecio(producto.price) }}
        <button @click="añadirProducto(producto)">Añadir al Carrito</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { inject } from 'vue';

const productos = inject('productos');
const añadirAlCarrito = inject('añadirAlCarrito');
const calcularPrecio = inject('calcularPrecio');

const añadirProducto = (producto) => {
  añadirAlCarrito(producto);
};
</script>
