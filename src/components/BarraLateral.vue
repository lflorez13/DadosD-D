<template>
    <!-- La barra lateral cambia de clase si 'sidebarOpen' es verdadero -->
    <div class="sidebar" :class="{ open: sidebarOpen }">
      <!-- Solo se muestra esta sección si 'sidebarOpen' es verdadero -->
      <div v-if="sidebarOpen" class="detailed-history">
        <h2>Historial de Lanzamientos</h2>
        <!-- Ciclo para mostrar el historial de lanzamientos-->
        <ul>
          <li v-for="(entry, index) in history" :key="'detail-' + index">
             <!-- Muestra cada lanzamiento en la lista del historial -->
            Lanzamiento {{ index + 1 }}:
            <span v-for="(value, dieIndex) in entry" :key="'die-' + dieIndex">
              <!-- Muestra el valor de cada dado en el lanzamiento correspondiente -->
              D{{ dieIndex + 1 }}: {{ value }}<span v-if="dieIndex < entry.length - 1">, </span>
            </span>
          </li>
        </ul>
        <!-- Botón para limpiar el historial, emite un evento 'clear-history' -->
        <button @click="$emit('clear-history')">Limpiar Historial</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      sidebarOpen: Boolean,
      history: Array
    }
  };
  </script>
  
  <style scoped>

  h2{
    color:blanchedalmond
  }
  .sidebar { /* Estilo de la barra */
    position: fixed;
    right: 0;
    top: 0;
    width: 300px;
    height: 100%;
    background-color: #000000a1;
    box-shadow: -2px 0 5px rgba(255, 255, 255, 0.3);
    overflow-y: auto;
    transition: transform 0.3s ease;
    transform: translateX(100%);
  }
  
  .sidebar.open {
    transform: translateX(0);
  }
  
  .detailed-history {
    padding: 20px;
    color:white
  }
  
  .detailed-history h2 {
    margin: 0;
    font-family: 'Georgia', sans-serif;
    font-weight: bolder;
  }
  
  .detailed-history ul {
    list-style-type: none;
    padding: 0;
  }
  
  .detailed-history li {
    margin-bottom: 10px;
  }
  
  button { /* Estilo boton limpiar historial  */
    font-family: 'Georgia', sans-serif;
    font-weight: bolder;
    font-size: 12px;
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #0f4f3b;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0d3d2c;
  }
  </style>