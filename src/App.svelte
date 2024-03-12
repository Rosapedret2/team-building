<!-- App.svelte -->
<script>
  import { onMount } from 'svelte';
  import TestA from './lib/TestA.svelte';
  import TestB from './lib/TestB.svelte';

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
    }
  });
</script>

<main>
  <h1>Bienvenido a tu aplicación</h1>
  <button on:click={empezarTestA}>Empezar TestA</button>
  <button on:click={empezarTestB}>Empezar TestB</button>

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
    background-color: black;
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
