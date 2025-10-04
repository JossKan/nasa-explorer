<script setup>
import { ref } from 'vue'
import PantallaBienvenida from './components/PantallaBienvenida.vue'
import PantallaMenu from './components/PantallaMenu.vue'

// Estados reactivos
const mostrarBienvenida = ref(true)
const quitarBlur = ref(false)
const mostrarMenu = ref(false)

// Función que maneja la transición entre pantallas
const handleComenzar = () => {
  // 1. Ocultar pantalla de bienvenida
  mostrarBienvenida.value = false
  
  // 2. Quitar blur después de 600ms (cuando termine la salida del texto)
  setTimeout(() => {
    quitarBlur.value = true
  }, 600)
  
  // 3. Mostrar menú después de 1400ms (cuando termine el blur)
  setTimeout(() => {
    mostrarMenu.value = true
  }, 1400)
}
</script>

<script>
import OpenSeadragon from "openseadragon";

export default {
  data() {
    return {
      viewer: null
    }
  },
  mounted() {
    this.viewer = OpenSeadragon({
      id: "viewer",
      prefixUrl: "https://openseadragon.github.io/openseadragon/images/",
      tileSources: "src/img/luneta_dos.dzi",
      
      showNavigator: true,
      defaultZoomLevel: 1,
      minZoomLevel: 0.5,
      maxZoomLevel: 10,
      visibilityRatio: 1.0,
      constrainDuringPan: false,
      zoomPerScroll: 1.3,
      gestureSettingsMouse: {
        clickToZoom: true,
        dblClickToZoom: true,
        scrollToZoom: true
      }
    });

    // Agregar manejador de clic para etiquetas
    // this.viewer.addHandler('canvas-click', this.onCanvasClick);

    // Cargar etiquetas guardadas
    this.viewer.addHandler('open', () => {
      this.loadTags();
    });
  },
  methods: {
    onCanvasClick(event) {
      let comment = prompt("¿Qué has encontrado? (Ej: Posible supernova, galaxia espiral)");
      if (!comment) return;

      let viewportPoint = this.viewer.viewport.pointFromPixel(event.position);
      let newTag = { x: viewportPoint.x, y: viewportPoint.y, text: comment };
      this.saveTag(newTag);
      this.drawTag(newTag);
    },
    saveTag(tag) {
      let tags = JSON.parse(localStorage.getItem('tags')) || [];
      tags.push(tag);
      localStorage.setItem('tags', JSON.stringify(tags));
    },
    drawTag(tag) {
      let tagElement = document.createElement("div");
      tagElement.className = "tag";
      tagElement.style.width = "10px";
      tagElement.style.height = "10px";
      tagElement.style.backgroundColor = "red";
      tagElement.style.borderRadius = "50%";
      tagElement.title = tag.text;

      this.viewer.addOverlay({ element: tagElement, location: new OpenSeadragon.Point(tag.x, tag.y) });

      const list = document.getElementById('tag-list');
      const listItem = document.createElement('li');
      listItem.textContent = tag.text;
      listItem.onclick = () => {
        this.viewer.viewport.panTo(new OpenSeadragon.Point(tag.x, tag.y));
        this.viewer.viewport.zoomTo(5);
      };
      list.appendChild(listItem);
    },
    loadTags() {
      const list = document.getElementById('tag-list');
      list.innerHTML = '';
      let tags = JSON.parse(localStorage.getItem('tags')) || [];
      tags.forEach(tag => this.drawTag(tag));
    }
  }
}
</script>


<template>
  <div>
    <!-- Fondo del espacio con transición de blur -->
    <div 
      class="FondoEspacio" 
      :class="{ 'sin-blur': quitarBlur }"
    ></div>

    <!-- Luna con transición de blur -->
    <div 
      class="LunaFondo"
      :class="{ 'sin-blur': quitarBlur }" style="text-align: right; width: 84%; padding-left: 16%;"
    >
    <div id="viewer" style="width:100%; height:100%; text-align: left;"></div>
    <ul id="tag-list"></ul>
    </div>

    <!-- Pantalla de bienvenida (primera pantalla) -->
    <Transition name="slide-up">
      <PantallaBienvenida 
        v-if="mostrarBienvenida"
        @comenzar="handleComenzar"
      />
    </Transition>

    <!-- Pantalla del menú (segunda pantalla) -->
    <Transition name="fade">
      <PantallaMenu v-if="mostrarMenu" />
    </Transition>
  </div>
</template>

<style scoped>
.FondoEspacio {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-image: url('');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  filter: blur(8px);
  z-index: 0;
  background-color: black;
  transition: filter 0.8s ease-out;  /* ⬅️ Asegúrate que esté aquí */
}

.FondoEspacio.sin-blur {  /* ⬅️ Verifica que esta clase exista */
  filter: blur(0px);
}

.LunaFondo {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url('');
  background-size: 95%;
  background-position: center;
  background-repeat: no-repeat;
  filter: blur(8px);
  z-index: 1;
  transition: filter 0.8s ease-out, 
              background-size 0.8s ease-out, 
              background-position 0.8s ease-out;
}


.LunaFondo.sin-blur {
  filter: blur(0px);
  background-size: 30%;
  background-position: 65% center;  
}

/* Transición para la salida de PantallaBienvenida (slide up) */
.slide-up-leave-active {
  transition: all 0.6s ease-out;
}

.slide-up-leave-to {
  transform: translateY(-100px);
  opacity: 0;
}

/* Transición para la entrada de PantallaMenu (fade in) */
.fade-enter-active {
  transition: opacity 0.8s ease-in;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-to {
  opacity: 1;
}
</style>