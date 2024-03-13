<script>
    // @ts-nocheck
  
    import { onMount } from 'svelte';
    import { select } from 'd3-selection';
    import { scaleLinear } from 'd3-scale';
    import { axisBottom, axisLeft } from 'd3-axis';
    import circulo from '../assets/circulo.jpg';
  
    let width = 400;
    let height = 400;
  
    let svg;
  
    const resultadoTestA = JSON.parse(localStorage.getItem('resultadoTestA'));
    const resultadoTestB = JSON.parse(localStorage.getItem('resultadoTestB'));
    
    // Verificar si los resultados están disponibles y establecerlos en 0 si no lo están
    const posicionX = resultadoTestA !== null ? resultadoTestA : 0;
    const posicionY = resultadoTestB !== null ? resultadoTestB : 0;
  
    let puntoAX, puntoAY, puntoBX, puntoBY;
    let resultadoA, resultadoB;
  
    onMount(() => {
      svg = select('#chart')
        .append('svg')
        .attr('width', width)
        .attr('height', height);
  
      const xScale = scaleLinear()
        .domain([-30, 30])
        .range([0, width]);
  
      const yScale = scaleLinear()
        .domain([-30, 30])
        .range([height, 0]);
  
      // Eje X
      svg.append('g')
        .attr('transform', `translate(0, ${height / 2})`)
        .call(axisBottom(xScale));
  
      // Eje Y
      svg.append('g')
        .attr('transform', `translate(${width / 2}, 0)`)
        .call(axisLeft(yScale));
  
      // Calcular la posición del punto en el gráfico para el Test A
      puntoAX = xScale(posicionX);
      puntoAY = height / 2; // El punto A está centrado verticalmente
  
      // Calcular la posición del punto en el gráfico para el Test B
      puntoBX = width / 2; // El punto B está centrado horizontalmente
      puntoBY = yScale(posicionY);
  
      // Calcular resultados
      resultadoA = `Resultado del Test A: ${posicionX}`;
      resultadoB = `Resultado del Test B: ${posicionY}`;
  
      // Dibujar los puntos
      svg.append('circle')
        .attr('cx', puntoAX)
        .attr('cy', puntoAY)
        .attr('r', 5)
        .attr('fill', 'red');
  
      svg.append('circle')
        .attr('cx', puntoBX)
        .attr('cy', puntoBY)
        .attr('r', 5)
        .attr('fill', 'blue');
      
      // Dibujar el círculo dividido en cuatro partes
      svg.append('circle')
        .attr('cx', width / 2)
        .attr('cy', height / 2)
        .attr('r', Math.min(width, height) / 2)
        .attr('fill', 'url(#gradient1)')
        .attr('opacity', 0.7);
    });
  </script>
  
  <main>
    <h1>Resultados</h1>
    <div id="chart"></div>
    <img class=circulo src={circulo} alt="circulo">
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
  
    .coordenadas {
      font-size: 16px;
    }
  </style>
  