<template>
    <div>
      <h2>Seleccionar Divisa</h2>
      <select v-model="divisaSeleccionada" @change="cambiarDivisa">
        <option value="EUR">€ Euros</option>
        <option value="USD">$ Dólares</option>
      </select>
    </div>
  </template>
  
  <script setup>
  import { inject } from 'vue';
  
  const divisaSeleccionada = inject('divisaSeleccionada');
  const tipoCambio = inject('tipoCambio');
  
  // Cambiar el tipo de cambio de forma sencilla
  const cambiarDivisa = () => {
    tipoCambio.value = divisaSeleccionada.value === 'USD' ? 1.1 : 1;
  };
  </script>
  