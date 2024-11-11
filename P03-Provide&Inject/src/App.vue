<template>
  <div class="Xat">
    <h1>{{ titulo }}</h1>
    <input v-model="titulo" placeholder="Escribe el nombre de la comanda" />

    
    <Divisa />
    <Producte @añadir-al-carrito="añadirAlCarrito" />
    <List />
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';
import Producte from './components/Producte.vue';
import List from './components/List.vue';
import Divisa from './components/Divisa.vue';

const titulo = ref('');
const cart = ref([]);

// Lista de productos
const productos = ref([
  { name: "Hamburguesa 🍔", price: 5 },
  { name: "Cheeseburger 🧀", price: 6 },
  { name: "Veggie Burger 🥕", price: 7 },
  { name: "Patatas 🍟", price: 2 }
]);

// Variables para la divisa
const divisaSeleccionada = ref('EUR');
const tipoCambio = ref(1);

// Proveer datos a componentes hijos
provide('productos', productos);
provide('cart', cart);
provide('divisaSeleccionada', divisaSeleccionada);
provide('tipoCambio', tipoCambio);

// Función para añadir productos al carrito
const añadirAlCarrito = (producto) => {
  cart.value.push(producto);

  // Mostrar alerta con todos los productos en el carrito
  const productosCarrito = cart.value.map(p => `${p.name} - ${calcularPrecio(p.price)}`).join('\n');
  alert(`Productos en el carrito:\n${productosCarrito}`);
};

// Función para calcular el precio con más detalle
const calcularPrecio = (precio) => {
  let precioConvertido = precio;
  // Si la divisa seleccionada es USD, aplicamos el tipo de cambio
  if (divisaSeleccionada.value === 'USD') {
    precioConvertido = precio * tipoCambio.value;
  } 
  // Si es EUR, no cambiamos el precio (ya está en euros)
  else if (divisaSeleccionada.value === 'EUR') {
    precioConvertido = precio; 
  }
  // Redondear el precio a 2 decimales
  precioConvertido = precioConvertido.toFixed(2);
  // Añadir el símbolo de la divisa al precio
  let precioFinal = '';
  if (divisaSeleccionada.value === 'USD') {
    precioFinal = `${precioConvertido} $`;
  } else if (divisaSeleccionada.value === 'EUR') {
    precioFinal = `${precioConvertido} €`;
  }

  return precioFinal;
};

provide('añadirAlCarrito', añadirAlCarrito);
provide('calcularPrecio', calcularPrecio);
</script>
