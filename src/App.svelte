<!-- App.svelte -->
<script>
  import { onMount } from 'svelte';
  import TestA from './lib/TestA.svelte';
  import TestB from './lib/TestB.svelte';
  import Resultados from './lib/Resultados.svelte';

  let currentComponent;

  function empezarTestA() {
    window.location.href = '/testA';
  }

  function empezarTestB() {
    window.location.href = '/testB';
  }

  onMount(() => {
    // Verifica la ruta actual y establece el componente correspondiente
    const currentPath = window.location.pathname;
    if (currentPath === '/testA') {
      currentComponent = TestA;
    } else if (currentPath === '/testB') {
      currentComponent = TestB;
    } else if (currentPath === '/resultados') {
      // Si la ruta actual es la de resultados, cargar los resultados
      currentComponent = Resultados;
    }
  });

  function mostrarResultados() {
    // Verificar si ambos tests están completos
    const resultadosTestA = JSON.parse(localStorage.getItem('resultadoTestA'));
    const resultadosTestB = JSON.parse(localStorage.getItem('resultadoTestB'));

    if (resultadosTestA !== null && resultadosTestB !== null) {
      // Redirigir a la página de resultados
      window.location.href = '/resultados';
    } else {
      alert('Aún no has completado ambos tests.');
    }
  }

  function limpiarResultados() {
    // Limpiar los resultados del almacenamiento local
    localStorage.removeItem('resultadosTestA');
    localStorage.removeItem('resultadosTestB');
  }
</script>

<main>
  <h1>TEST PERSONALIDAD</h1>
  <button on:click={empezarTestA}>Empezar TestA</button>
  <button on:click={empezarTestB}>Empezar TestB</button>
  <button on:click={mostrarResultados}>Ver Resultados</button>

  {#if currentComponent}
    <svelte:component this={currentComponent} />
  {/if}
</main>

<style>
  /* Estilos según tus preferencias */
  h1 {
    color: red;
  }

  main {
    background-color: white;
    padding: 20px; /* Añade espacio alrededor del contenido */
  }

  button {
    margin: 10px; /* Añade espacio entre los botones y el título */
    padding: 8px 16px;
    font-size: 16px;
    background-color: #4caf50; /* Color de fondo verde */
    color: white; /* Color del texto blanco */
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049; /* Cambia el color de fondo al pasar el ratón sobre el botón */
  }
</style>
