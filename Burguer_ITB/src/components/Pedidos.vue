<script setup>
// Importamos funciones que utilizaremos:
import { inject, defineEmits } from 'vue';

// Inyectamos productos y la moneda:
const productos = inject('productos');
const currency = inject('currency');

// Emitimos eventos
const emit = defineEmits();

// Creamos la funcion para formatear precio
function formateoDePrecios(precio) {
   // Formateamos precio usando la moneda seleccionada y aseguramos que tenga dos decimales (para conseguir .00):
   return `${currency.value}${precio.toFixed(2)}`;
}

// Creamos la función para manejar el evento de añadir al carro
function addToCart(product) {
   // Emitimos un evento 'product-added' con el nombre del producto seleccionado
   emit('product-added', product.name); // Emitir el nombre del producto
}
</script>



<template>
   <div v-for="product in productos" :key="product.name">
     <span>{{ product.name }}: {{ formateoDePrecios(product.price) }}</span>
     <button @click="addToCart(product)">Add to Cart</button>
   </div>
</template>


