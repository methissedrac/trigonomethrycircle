
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    canvas {
      border: 1px solid #000;
      background-color: #f8f8f8;
    }
  </style>
</head>

<body>


  <canvas id="circleCanvas" width="400" height="400"></canvas>
  <input type="button" id="piButton" value="π" />
  <input type="text" id="inputValue" placeholder="Enter angle or expression" />
  <button onclick="drawPoint()">Draw Point</button>

<script>
   const canvas = document.getElementById('circleCanvas');
    const ctx = canvas.getContext('2d');
    const radius = 150;
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const gridSize = 20;

    // Draw a grid
    function drawGrid() {
      ctx.beginPath();
      for (let x = gridSize; x < canvas.width; x += gridSize) {
        ctx.moveTo(x, 0);
        ctx.lineTo(x, canvas.height);
      }

      for (let y = gridSize; y < canvas.height; y += gridSize) {
        ctx.moveTo(0, y);
        ctx.lineTo(canvas.width, y);
      }

      ctx.strokeStyle = '#ddd';
      ctx.stroke();
    }

    // Draw the unit circle
    function drawCircle() {
      ctx.beginPath();
      ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
      ctx.strokeStyle = '#000';
      ctx.stroke();
    }

    // Clear previous point and grid
    function clearCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawGrid();    // Redraw grid after clearing
      drawCircle();  // Redraw circle after clearing
    }

    // Draw a point on the circle at the given angle in radians
    function drawPoint() {
      let inputValue = document.getElementById('inputValue').value;
      // Replace π symbol with Math.PI and evaluate the expression
      let angleInRadians = 0;
      if (inputValue.trim() !== '') {
        inputValue = inputValue.replace(/π/g, 'Math.PI');
        try {
          angleInRadians = eval(inputValue);
        } catch {
          alert("Invalid expression");
          return;
        }
      }

      const x = centerX + radius * Math.cos(angleInRadians);
      const y = centerY - radius * Math.sin(angleInRadians);

      clearCanvas();  // Clear before drawing new point

      ctx.fillStyle = '#ff0000';
      ctx.beginPath();
      ctx.arc(x, y, 5, 0, 2 * Math.PI);
      ctx.fill();
    }

    // Insert Pi symbol into the input when clicked
    document.getElementById('piButton').addEventListener('click', function () {
      document.getElementById('inputValue').value += 'π';
    });

    // Initial draw
    drawGrid();
    drawCircle();
  </script>


</body>

</html>
