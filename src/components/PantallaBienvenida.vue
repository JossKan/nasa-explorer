<script setup>
const emit = defineEmits(['comenzar'])

const iniciarViaje = () => {
  emit('comenzar')
}
</script>

<template>
  <div class="ContenidoInicio">
    <div class="ContenidoCentral">
      <p class="Subtitulo">NASA EXPLORER</p>
      <h1 class="TextoBienvenida">Explora el Universo</h1>
      <p class="Descripcion">Descubre imágenes fascinantes del cosmos</p>
      <button class="BotonInicio" @click="iniciarViaje">
        Comenzar exploración
        <span class="Flecha">→</span>
      </button>
    </div>
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
  padding: 1rem;
}

.ContenidoCentral {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  text-align: center;
  max-width: 90%;
}

/* Animación de entrada */
@keyframes fadeInUp {
  from {
    transform: translateY(30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.Subtitulo {
  animation: fadeInUp 0.8s ease-out forwards;
  font-size: clamp(0.7rem, 2vw, 0.85rem);
  letter-spacing: 2px;
  color: rgba(255, 255, 255, 0.7);
  margin: 0;
  font-weight: 500;
}

.TextoBienvenida {
  animation: fadeInUp 0.8s ease-out 0.2s forwards;
  opacity: 0;
  font-size: clamp(2.5rem, 8vw, 4.5rem);
  font-weight: 300;
  color: white;
  margin: 0;
  line-height: 1.1;
}

.Descripcion {
  animation: fadeInUp 0.8s ease-out 0.4s forwards;
  opacity: 0;
  font-size: clamp(0.95rem, 3vw, 1.1rem);
  color: rgba(255, 255, 255, 0.8);
  margin: 0.5rem 0 2rem 0;
  font-weight: 300;
  max-width: 600px;
}

.BotonInicio {
  animation: fadeInUp 0.8s ease-out 0.6s forwards;
  opacity: 0;
  padding: clamp(0.8rem, 2vw, 1rem) clamp(1.8rem, 4vw, 2.5rem);
  font-size: clamp(0.9rem, 2vw, 1rem);
  background: white;
  border: none;
  color: #1a1a1a;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: 500;
  white-space: nowrap;
}

.Flecha {
  transition: transform 0.3s ease;
  font-size: clamp(1rem, 2vw, 1.2rem);
}

.BotonInicio:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 30px rgba(255, 255, 255, 0.3);
}

.BotonInicio:hover .Flecha {
  transform: translateX(5px);
}

/* Tablets */
@media (max-width: 768px) {
  .ContenidoCentral {
    gap: 0.8rem;
  }
  
  .Subtitulo {
    letter-spacing: 1.5px;
  }
  
  .Descripcion {
    margin: 0.3rem 0 1.5rem 0;
  }
}

/* Móviles */
@media (max-width: 480px) {
  .ContenidoInicio {
    padding: 1.5rem;
  }
  
  .ContenidoCentral {
    gap: 0.6rem;
    max-width: 100%;
  }
  
  .Subtitulo {
    letter-spacing: 1px;
  }
  
  .TextoBienvenida {
    line-height: 1.2;
  }
  
  .Descripcion {
    margin: 0.2rem 0 1.2rem 0;
  }
  
  .BotonInicio:hover {
    /* Reducir efecto en móviles táctiles */
    transform: scale(1.02);
  }
}

/* Móviles pequeños */
@media (max-width: 360px) {
  .ContenidoInicio {
    padding: 1rem;
  }
  
  .BotonInicio {
    font-size: 0.85rem;
  }
}

/* Pantallas muy grandes */
@media (min-width: 1920px) {
  .TextoBienvenida {
    font-size: 5.5rem;
  }
  
  .Descripcion {
    font-size: 1.3rem;
  }
}
</style>