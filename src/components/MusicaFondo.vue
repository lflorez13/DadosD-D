<template>
    <div class="musica-container">
      <audio ref="audioPlayer" :src="musicaSrc" controls>
        Tu navegador no soporta el elemento de audio.
      </audio>

    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        musicaSrc: require('@/assets/audioD_D.mp3'), // Reemplaza 'tu-musica.mp3' con el nombre de tu archivo
        isPlaying: false
      };
    },
    methods: {
      togglePlay() {
        const audio = this.$refs.audioPlayer;
        if (this.isPlaying) {
          audio.pause();
        } else {
          audio.play();
        }
        this.isPlaying = !this.isPlaying;
      }
    }
  };
  </script>
  
  <style scoped>
  .musica-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  /*button {
    font-family: 'Georgia', sans-serif;
    font-weight: bolder;
    font-size: 12px;
    margin-top: 10px;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }*/
  </style>