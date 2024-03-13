<!-- src/lib/TestB.svelte -->
<script>
  import { onMount } from "svelte";
  import Chart from 'chart.js/auto';

  let casosB = [
    { frasePositiva: "Tengo éxito", fraseNegativa: "Soy un fracaso", valorSeleccionado: null },
    { frasePositiva: "Soy feliz", fraseNegativa: "Soy infeliz", valorSeleccionado: null },
    { frasePositiva: "Soy saludable", fraseNegativa: "Soy enfermo", valorSeleccionado: null },
    { frasePositiva: "Soy valioso", fraseNegativa: "Soy inútil", valorSeleccionado: null },
    { frasePositiva: "Soy amado", fraseNegativa: "Soy rechazado", valorSeleccionado: null },
    { frasePositiva: "Soy exitoso", fraseNegativa: "Soy un fracaso", valorSeleccionado: null }
  ];

  let sumaTotalB = 0;
  let todosCasosCompletosB = false;

  // Datos para el gráfico circular
  let resultadosB = {};

  let ctxB; // Declarar la variable ctxB aquí

  function seleccionarValorB(caso, valor) {
    caso.valorSeleccionado = valor;
    calcularSumaTotalB();
    verificarCasosCompletosB();
    actualizarResultadosB();
  }

  function calcularSumaTotalB() {
    sumaTotalB = casosB.reduce((total, caso) => total + (caso.valorSeleccionado || 0), 0);
  }

  function verificarCasosCompletosB() {
    todosCasosCompletosB = casosB.every(caso => caso.valorSeleccionado !== null);
    if (todosCasosCompletosB) {
      // Guardar el resultado en el almacenamiento local
      localStorage.setItem('resultadoTestB', sumaTotalB);
    }
  }

  function actualizarResultadosB() {
    resultadosB = {
      "Resultado": sumaTotalB
    };
  }

  $: {
    if (todosCasosCompletosB) {
      const labels = Object.keys(resultadosB);
      const data = Object.values(resultadosB);

      const chartData = {
        labels: labels,
        datasets: [
          {
            data: data,
            backgroundColor: data.map(value => (value < 0 ? "red" : "blue"))
          }
        ]
      };

      const chartConfig = {
        type: "doughnut",
        data: chartData,
        options: {
          cutout: '70%',
          plugins: {
            legend: {
              display: false
            }
          }
        }
      };

      const chart = new Chart(ctxB, chartConfig);
    }
  }
</script>

<main>
  <h1>Bienvenido a la prueba TestB</h1>

  {#each casosB as caso}
    <div class="test-container">
      <div class="frase">{caso.frasePositiva}</div>
      <div class="valores">
        {#each Array.from({ length: 11 }, (_, i) => i - 5) as valor}
          <button
            class:seleccionado={caso.valorSeleccionado === valor}
            on:click={() => seleccionarValorB(caso, valor)}
          >{valor}</button>
        {/each}
      </div>
      <div class="frase">{caso.fraseNegativa}</div>
      <div class="respuesta">Respuesta seleccionada: {caso.valorSeleccionado || 'Ninguno'}</div>
    </div>
  {/each}

  {#if todosCasosCompletosB}
    <div class="suma-total">
      <div class="resultado-suma">Resultado de la suma: {sumaTotalB}</div>
      <canvas bind:this={ctxB}></canvas>
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
  .frase{
    color: aliceblue;
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
