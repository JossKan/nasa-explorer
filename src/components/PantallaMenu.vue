<script setup>
// Script vacío por ahora (después agregarás la lógica del menú desplegable)
</script>

<template>
  <div class="ContenedorMenu">
    <!-- Menú lateral izquierdo -->
    <aside class="MenuLateral">
      <h3>Menú</h3>
      <nav>
        <ul>
          <li><a href="#">Marcadores</a></li>
          <li><a href="#">Comparar</a></li>
          <li><a href="#">Descargar</a></li>
          <li><a href="#">Despues</a></li>
        </ul>
      </nav>
    </aside>

    <!-- Área vacía para la luna -->
    <main class="ContenidoPrincipal"></main>
  </div>
</template>

<style scoped>
/* Contenedor principal */
.ContenedorMenu {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  display: flex;
  height: 100vh;
  width: 100%;
  pointer-events: none;
}

/* Menú lateral */
.MenuLateral {
  width: 180px;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(10px);
  border-right: 1px solid rgba(255, 255, 255, 0.2);
  padding: 2rem 1rem;
  color: white;
  overflow-y: auto;
  pointer-events: auto;
}

.MenuLateral h3 {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  text-align: center;
  color: white;
}

.MenuLateral nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.MenuLateral nav li {
  margin-bottom: 1rem;
}

.MenuLateral nav a {
  display: block;
  padding: 0.75rem 1rem;
  color: white;
  text-decoration: none;
  border-radius: 8px;
  transition: all 0.3s ease;
  background: rgba(255, 255, 255, 0.05);
}

.MenuLateral nav a:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateX(5px);
}

/* Contenido principal (área vacía para la luna) */
.ContenidoPrincipal {
  flex: 1;
}
</style>