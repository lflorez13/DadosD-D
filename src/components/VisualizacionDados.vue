<template>
  <!-- Se muestra este contenedor solo si hay dados en la lista -->
  <div v-if="dice.length" class="dice-container">
    <div class="dice-row">
      <!-- Ciclo para mostrar los botones de + y -, y las imagenes de cada dado -->
      <div v-for="(die, index) in dice" :key="index" class="dice-item">
        <img :src="getDieImage(results[index])" :alt="'Dado ' + results[index]" />
        <div class="controls">
          <!-- Botón para disminuir el número de caras del dado -->
          <button @click="$emit('decrease-sides', index)" :disabled="die <= 4">-</button>
          <!-- Muestra el número de caras del dado -->
          <span class="dice-sides">{{ die }} caras</span>
          <!-- Botón para aumentar el número de caras del dado -->
          <button @click="$emit('increase-sides', index)" :disabled="die >= 12">+</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dice: Array,
    results: Array
  },
  methods: { 
    getDieImage(value) {
      return value === 0 ? require('@/assets/0.png') : require(`@/assets/${value}.png`);
      /* Retorna la imagen de cada dado, dependiendo del numero del ciclo for en template */
    }
  }
};
</script>

<style scoped>

.dice-sides { /* Estilo de la letra del numero de caras */
  font-family: 'Georgia', sans-serif;
  font-size: 14px; 
  font-weight:900; 
  margin: 0 5px;
  color:rgb(255, 255, 255)
}

.dice-container {
  text-align: center;
  margin-top: 20px;
}

.dice-row {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.dice-item {
  margin: 5px;
  text-align: center;
}

.dice-item img { /* Dimensiones de dados */
  width: 135px;
  height: 135px;
  margin-left: 5px;
  margin-right: 5px;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 5px;
}

.controls button { 
  margin: 0 5px;
  padding: 5px 10px;
}
</style>