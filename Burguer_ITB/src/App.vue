<script setup>
  // Importamos funciones necesarias de Vue en m icaso ref y provide:
  import { ref, provide } from 'vue';
  // Importamos componente Pedidos que lo usare para mostrar los productos:
  import Pedidos from './components/Pedidos.vue';


  // Definimos moneda inicial que se usará:
  const currency = ref('$');

  // Creamos el array de productos con name y price
  const productos = ref([
    { name: "Hamburger 🍔.", price: 5 },
    { name: "Cheeseburger 🧀", price: 6 },
    { name: "Impossible Burger 🥕", price: 7 },
    { name: "Fries 🍟", price: 2 }
  ]);

  // Estado para el nombre del pedido introducido por el usuario
  const nombrePedido = ref("");
  // Estado para almacenar los productos que el usuario ha añadido al carrito
  const productosComprados = ref([]);


  // Proporcionamos los productos y la moneda a los componentes hijos
  provide('productos', productos);
  provide('currency', currency);


  // Creamos la función para manejar cuando se añade un producto al carrito
  function manejarProductoAñadido(nombreProducto) {
      // Añadimos nombre del producto al array:  
      productosComprados.value.push(nombreProducto); // Añadir el nombre del producto al array
      // Construimos mensaje de alerta:
      const alertMessage = `${productosComprados.value.join(', ')}`;
      // Mostramos mensaje:
      alert(alertMessage);  
  }

  function manejarPedidoRealizado() {
      // Mostramos mensaje indicando que el pedido ha sido realizado:
      alert('Tu pedido ha sido realizado');
  }
</script>

<template>
  <h1>{{ nombrePedido }}</h1>
  <input v-model="nombrePedido" type="text" placeholder="Escribe tu nombre de pedido">
  <button @click="manejarPedidoRealizado">Realizar pedido</button>
  
  <label>
    Currency
    <select v-model="currency">
      <option value="€">Euros(€)</option>
      <option value="$">Dollars($)</option>
    </select>
  </label>

  <Pedidos @product-added="manejarProductoAñadido" />
</template>






<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
