<!-- src/lib/Resultados.svelte -->
<script>
    // Obtener los resultados de los tests del almacenamiento local
    const resultadoTestA = JSON.parse(localStorage.getItem('resultadoTestA'));
    const resultadoTestB = JSON.parse(localStorage.getItem('resultadoTestB'));
  
    // Verificar si los resultados están disponibles y establecerlos en 0 si no lo están
    const posicionX = resultadoTestA !== null ? resultadoTestA : 0;
    const posicionY = resultadoTestB !== null ? resultadoTestB : 0;
  
    // Calcular la posición del punto en el gráfico para el Test A
    const puntoAX = mapToRange(posicionX, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
    const puntoAY = mapToRange(posicionX, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
  
    // Calcular la posición del punto en el gráfico para el Test B
    const puntoBX = mapToRange(posicionY, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
    const puntoBY = mapToRange(posicionY, -30, 30, 0, 400); // Mapear desde -30 a 30 a 0 a 400
  
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
      <div class="valores-eje-x" style="left: 75px; bottom: 200px;">-20</div>
      <div class="valores-eje-x" style="left: 150px; bottom: 200px;">-10</div>
      <div class="valores-eje-x" style="left: 225px; bottom: 200px;">0</div>
      <div class="valores-eje-x" style="left: 300px; bottom: 200px;">10</div>
      <div class="valores-eje-x" style="left: 375px; bottom: 200px;">20</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 0;">-30</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 75px;">-20</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 150px;">-10</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 225px;">0</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 300px;">10</div>
      <div class="valores-eje-y" style="left: 200px; bottom: 375px;">20</div>
      <!-- Punto de resultado Test A -->
      <div class="puntoA" style="left: {puntoAX}px; bottom: {puntoAY}px;"></div>
      <!-- Punto de resultado Test B -->
      <div class="puntoB" style="left: {puntoBX}px; bottom: {puntoBY}px;"></div>
    </div>
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
  </style>
  