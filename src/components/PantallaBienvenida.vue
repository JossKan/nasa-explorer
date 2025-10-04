<script setup>
// Ya no necesitas imports ni refs, solo defines el emit
const emit = defineEmits(['comenzar'])

// Función que se ejecuta cuando hacen click en el botón
const iniciarViaje = () => {
  emit('comenzar')  // Emite el evento hacia App.vue
}
</script>

<template>
  <!-- Solo el contenido de la pantalla inicial -->
  <div class="ContenidoInicio">
    <h1 class="TextoBienvenida">Empezemos el viaje</h1>
    <button class="BotonInicio" @click="iniciarViaje">Comenzemos</button>
  </div>
</template>

<style scoped>
.ContenidoInicio {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  gap: 2rem;
}

/* Animación de entrada (slideDown) */
@keyframes slideDown {
  from {
    transform: translateY(-100px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.TextoBienvenida {
  animation: slideDown 1s ease-out forwards;
  font-size: 3rem;
  color: white;
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
  margin: 0;
}

.BotonInicio {
  animation: slideDown 1s ease-out 0.5s forwards;
  opacity: 0;
  padding: 1rem 2.5rem;
  font-size: 1.2rem;
  background: rgba(255, 255, 255, 0.1);
  border: 2px solid white;
  color: white;
  border-radius: 50px;
  cursor: pointer;
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

.BotonInicio:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.05);
}
</style>