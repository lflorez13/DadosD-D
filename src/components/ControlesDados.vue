<template>
  <div class="controls-container">
    <!-- Se agregan los 3 botones de arriba  -->
    <button @click="$emit('add-die')" :disabled="dice.length >= 6">Agregar Dado</button>
    <button @click="$emit('remove-die')" :disabled="dice.length <= 1">Eliminar Dado</button>
    <button @click="$emit('clear-dice')">Limpiar Dados</button>
  </div>
</template>

<script>
export default {
  props: {
    dice: Array
  }
};
</script>

<style scoped>
.controls-container {
  display: flex;
  justify-content: center; 
  margin-bottom: 20px; 
}

button { /* Estilo de los 3 botones */
  font-family: 'Georgia', sans-serif;
  font-weight: bolder;
  font-size: 12px;
  margin: 10px;
  margin-top: 1px;
  padding: 14px;
  border-radius: 10px;
}

button:hover {/* Estilo de los 3 botones cuando se da click */
  background-color: rgb(2, 2, 2);
  color: #e9e9e9;
  border-color: #000000;
  transform: scale(1.05);
}
</style>