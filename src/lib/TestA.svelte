<!-- src/lib/TestA.svelte -->
<script>
  import { onMount } from "svelte";
  import Chart from 'chart.js/auto';

  let casos = [
    { frasePositiva: "Soy guapa", fraseNegativa: "Soy fea", valorSeleccionado: null },
    { frasePositiva: "Soy alta", fraseNegativa: "Soy baja", valorSeleccionado: null },
    { frasePositiva: "Soy blanca", fraseNegativa: "Soy negra", valorSeleccionado: null },
    { frasePositiva: "Soy buena", fraseNegativa: "Soy mala", valorSeleccionado: null },
    { frasePositiva: "Soy gorda", fraseNegativa: "Soy delgada", valorSeleccionado: null },
    { frasePositiva: "Soy amable", fraseNegativa: "Soy borde", valorSeleccionado: null }
  ];

  let sumaTotal = 0;
  let todosCasosCompletos = false;

  // Datos para el gráfico de puntos
  let resultados = [];

  let ctx; // Declarar la variable ctx aquí

  function seleccionarValor(caso, valor) {
    caso.valorSeleccionado = valor;
    calcularSumaTotal();
    verificarCasosCompletos();
    actualizarResultados();
  }

  function calcularSumaTotal() {
    sumaTotal = casos.reduce((total, caso) => total + (caso.valorSeleccionado || 0), 0);
  }

  function verificarCasosCompletos() {
    todosCasosCompletos = casos.every(caso => caso.valorSeleccionado !== null);
    if (todosCasosCompletos) {
      // Guardar el resultado en el almacenamiento local
      localStorage.setItem('resultadoTestA', sumaTotal);
    }
  }

  function actualizarResultados() {
    resultados = [{
      x: sumaTotal, // Posición en el eje X
      y: 0// Posición en el eje Y (central)
    }];
  }

  $: {
    if (todosCasosCompletos) {
      const chartData = {
        datasets: [{
          label: 'Resultados',
          data: resultados,
          borderColor: 'rgba(54, 162, 235, 1)',
          backgroundColor: 'rgba(54, 162, 235, 1)',
          pointRadius: 8,
          pointHoverRadius: 10,
          pointStyle: 'circle' // Estilo de los puntos
        }]
      };

      const chartConfig = {
        type: "scatter",
        data: chartData,
        options: {
          scales: {
            x: {
              type: 'linear',
              position: 'bottom',
              min: -30, // Valor mínimo en el eje X
              max: 30, // Valor máximo en el eje X
              ticks: {
                stepSize: 5 // Espaciado entre los ticks
              }
            },
            y: {
              type: 'linear',
              position: 'left',
              min: -30, // Valor mínimo en el eje Y
              max: 30, // Valor máximo en el eje Y
              ticks: {
                stepSize: 5 // Espaciado entre los ticks
              }
            }
          }
        }
      };

      const chart = new Chart(ctx, chartConfig);
    }
  }
</script>

<main>
  <h1>Bienvenido a la prueba TestA</h1>

  {#each casos as caso}
    <div class="test-container">
      <div class="frase">{caso.frasePositiva}</div>
      <div class="valores">
        {#each Array.from({ length: 11 }, (_, i) => i - 5) as valor}
          <button
            class:seleccionado={caso.valorSeleccionado === valor}
            on:click={() => seleccionarValor(caso, valor)}
          >{valor}</button>
        {/each}
      </div>
      <div class="frase">{caso.fraseNegativa}</div>
      <div class="respuesta">Respuesta seleccionada: {caso.valorSeleccionado || 'Ninguno'}</div>
    </div>
  {/each}

  {#if todosCasosCompletos}
    <div class="suma-total">
      <div class="resultado-suma">Resultado de la suma: {sumaTotal}</div>
      <canvas bind:this={ctx}></canvas>
    </div>
  {/if}
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  h1 {
    margin-bottom: 20px;
  }

  .test-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 80%;
    margin-bottom: 20px;
  }

  .frase, .valores {
    flex: 1;
  }

  .valores button {
    margin: 5px;
    padding: 8px 12px;
    font-size: 14px;
    cursor: pointer;
  }

  .valores button.seleccionado {
    background-color: red;
    color: white;
  }

  .respuesta {
    margin-top: 20px;
  }

  .suma-total {
    margin-top: 30px;
    text-align: center;
  }

  .resultado-suma {
    font-size: 16px;
    font-weight: bold;
    color: red;
  }

  canvas {
    max-width: 200px; /* Ajusta el tamaño según tus necesidades */
    margin-top: 20px;
  }
</style>
