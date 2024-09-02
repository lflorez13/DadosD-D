<template>
  <div>
    <div class="title-container">
      <img src="@/assets/Imagen5.png" alt="Icono" class="title-icon" /> <!-- icono al lado del titulo -->
      <h1>DUNGEONS & DRANGONS</h1> <!-- Titulo -->
    </div>
    <!-- Se coloca los controles y los dados desde los otros componentes -->
    <ControlesDados :dice="dice" @add-die="addDie" @remove-die="removeDie" @clear-dice="clearDice" />
    <VisualizacionDados :dice="dice" :results="results" @increase-sides="increaseSides" @decrease-sides="decreaseSides" />
    <!-- Se coloca el boton de lanzar -->
    <button @click="rollDice" class="Lanzar">Lanzar</button>
    <!-- Se coloca el boton del historial -->
    <button @click="toggleSidebar" class="toggle-sidebar-button">
      {{ sidebarOpen ? 'Ocultar Historial de Lanzamientos' : 'Ver Historial de Lanzamientos' }}
    </button>
    <BarraLateral :sidebarOpen="sidebarOpen" :history="history" @clear-history="clearHistory" />
    <!-- Se coloca el boton de la musica de fondo desde el otro componente -->
    <MusicaFondo />
  </div>
</template>

<script>
import ControlesDados from './components/ControlesDados.vue';
import VisualizacionDados from './components/VisualizacionDados.vue';
import BarraLateral from './components/BarraLateral.vue';
import MusicaFondo from './components/MusicaFondo.vue';

export default {
  components: {
    /* Se importa todos los componentes */
    ControlesDados,
    VisualizacionDados,
    BarraLateral,
    MusicaFondo
  },
  data() {
    return {
      // Estado inicial: un dado de 6 caras, el resultado inicial en 0, el historial de resultados vacio
      // y la barra lateral cerrada
      dice: [6],
      results: [0], 
      history: [],  
      sidebarOpen: false 
    };
  },
  methods: {
    addDie() {
      // Agrega un dado al arreglo de dados y un valor inicial de 0 al arreglo de resultados,
      // si la cantidad de dados es menor a 6.
      if (this.dice.length < 6) {
        this.dice.push(6);
        this.results.push(0);
      }
    },
    removeDie() {
      // Elimina un dado si la cantidad de dados es mayor a 1
      if (this.dice.length > 1) {
        this.dice.pop();
        this.results.pop();
      }
    },
    clearDice() {
      // Restablece el estado inicial de los dados, con un solo dado de 6 caras
      this.dice = [6];
      this.results = [0];
    },
    rollDice() {
      //Genera un número aleatorio para cada dado basado en su cantidad de caras y actualiza el 
      //arreglo de resultados.
      this.results = this.dice.map((sides) => {
        return Math.floor(Math.random() * sides) + 1;
      });
      this.history.push([...this.results]); // Agrega los resultados al historial
    },
    increaseSides(index) {
      // Incrementa el número de caras de un dado específico en 2 hasta 12 
      if (this.dice[index] < 12) {
        this.dice[index] += 2;
      }
    },
    decreaseSides(index) {
      // Decrementa el número de caras de un dado específico en 2 hasta 4 
      if (this.dice[index] > 4) {
        this.dice[index] -= 2;
      }
    },
    clearHistory() {
      // Limpia el historial de resultados de lanzamientos.
      this.history = []; // Limpia el historial de resultados
    },
    toggleSidebar() {
      // Alterna la visibilidad de la barra lateral.
      this.sidebarOpen = !this.sidebarOpen; // Alterna la visibilidad de la barra lateral
    },
    formatHistoryEntry(entry) {
      // Formatea una entrada del historial en una cadena de texto separada por comas.
      return entry.join(', ');
    }
  }
};
</script>

<style scoped>



.title-container {
  display: flex;
  align-items: center;
  justify-content: center; /* Centrar el contenido horizontalmente */
  padding: 10px;
  color: #007BFF; /* Color del texto del título */
}

.title-icon {
  width: 120px; /* Tamaño de la imagen (ajusta según necesites) */
  height: 100px;
  margin-right: 10px; /* Espacio entre la imagen y el título */
}

h1 {
  font-family: 'Georgia', sans-serif;
  font-size: 50px;
  font-weight:bolder;
  color: rgb(255, 255, 255);
  text-align: center;
  padding: 0;
}

button {
  font-family: 'Georgia', sans-serif;
  font-weight: bolder;
  font-size: 12px;
  margin: 5px;
  padding: 12px;
  border-radius: 10px;
}

button:hover {
  background-color: rgb(2, 2, 2); /* Cambia el color de fondo al pasar el mouse */
  color: #e9e9e9;
  border-color: #000000; /* Cambia el color del borde al pasar el mouse */
  transform: scale(1.05); /* Efecto de agrandar */
}

.Lanzar {
  font-family: 'Georgia', sans-serif;
  font-weight: bolder;
  font-size: 18px;
  margin: 10px;
  padding: 10px 35px;
  border-radius: 10px;
  cursor: pointer;
  display: block;
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
}

.Lanzar:hover {
  background-color: rgba(233, 0, 0, 0.801); /* Cambia el color de fondo al pasar el mouse */
  color: #e9e9e9;
  border-color: #000000; /* Cambia el color del borde al pasar el mouse */
  transform: scale(1.05); /* Efecto de agrandar */
}

.toggle-sidebar-button {
  margin: 20px;
  padding: 10px 20px;
  background-color: #0f4f3b;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  display: block;
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
}

</style>