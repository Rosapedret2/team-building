<script>
  // Obtener los resultados de los tests del almacenamiento local
  const resultadoTestA = JSON.parse(localStorage.getItem('resultadoTestA'));
  const resultadoTestB = JSON.parse(localStorage.getItem('resultadoTestB'));

  // Verificar si los resultados están disponibles y establecerlos en null si no lo están
  const posicionX = resultadoTestA !== null ? resultadoTestA : null;
  const posicionY = resultadoTestB !== null ? resultadoTestB : null;

  let puntoAX = null;
  let puntoAY = null;
  let puntoBX = null;
  let puntoBY = null;

  // Calcular la posición del punto en el gráfico para el Test A
  if (posicionX !== null) {
    puntoAX = mapToRange(posicionX, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
    puntoAY = mapToRange(posicionX, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
  }

  // Calcular la posición del punto en el gráfico para el Test B
  if (posicionY !== null) {
    puntoBX = mapToRange(posicionY, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
    puntoBY = mapToRange(posicionY, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
  }

  // Función para mapear un valor de un rango a otro rango
  function mapToRange(value, fromLow, fromHigh, toLow, toHigh) {
    return (value - fromLow) * (toHigh - toLow) / (fromHigh - fromLow) + toLow;
  }
</script>

<main>
  <h1>Resultados</h1>
  <div class="grafico">
    <!-- Ejes del gráfico -->
    <div class="eje-x" style="left: 0; bottom: 200px; width: 400px;"></div>
    <div class="eje-y" style="left: 200px; bottom: 0; height: 400px;"></div>
    <!-- Valores de los ejes -->
    <div class="valores-eje-x" style="left: 0; bottom: 200px;">-30</div>
    <!-- Otros valores del eje X -->
    <div class="valores-eje-y" style="left: 200px; bottom: 0;">-30</div>
    <!-- Otros valores del eje Y -->
    
    <!-- Mostrar punto A si el resultado del Test A está disponible -->
    {#if posicionX !== null}
      <div class="puntoA" style="left: {puntoAX}px; bottom: {puntoAY}px;"></div>
    {/if}
    
    <!-- Mostrar punto B si el resultado del Test B está disponible -->
    {#if posicionY !== null}
      <div class="puntoB" style="left: {puntoBX}px; bottom: {puntoBY}px;"></div>
    {/if}
  </div>
  <!-- Mostrar mensaje si los tests no están completados -->
  {#if posicionX === null || posicionY === null}
    <div class="alerta">Por favor, complete los tests para ver los resultados.</div>
  {:else}
    <div class="coordenadas">
      Posición en el eje X (Test A): {posicionX}
      <br>
      Posición en el eje Y (Test B): {posicionY}
    </div>
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
<<<<<<< HEAD
  
    .grafico {
      position: relative;
      width: 400px; /* Ancho del gráfico */
      height: 400px; /* Alto del gráfico */
      margin-bottom: 20px;
    }
  
    .eje-x, .eje-y {
      position: absolute;
      background-color: black;
    }
  
    .eje-x {
      height: 1px;
      bottom: 200px; /* Posiciona el eje X en la parte inferior */
      left: 0;
      width: 400px;
    }
  
    .eje-y {
      width: 1px;
      left: 200px; /* Posiciona el eje Y en el centro */
      bottom: 0;
      height: 400px;
    }
  
    .valores-eje-x, .valores-eje-y {
      position: absolute;
      font-size: 12px;
      text-align: center;
    }
  
    .valores-eje-x {
      bottom: -12px; /* Centra los valores del eje X */
    }
  
    .valores-eje-y {
      left: -20px; /* Centra los valores del eje Y */
    }
  
    .puntoA, .puntoB {
      position: absolute;
      width: 10px; /* Ancho del punto */
      height: 10px; /* Alto del punto */
      border-radius: 50%; /* Hace que el punto sea redondo */
      transform: translate(-50%, -50%); /* Centra el punto en su posición */
    }
  
    .puntoA {
      background-color: red; /* Color del punto para el Test A */
    }
  
    .puntoB {
      background-color: blue; /* Color del punto para el Test B */
    }
  
    .coordenadas {
      font-size: 16px;
    }
=======

>>>>>>> d02097008c2730025af942f2820152c93e9550ce
  </style>
  