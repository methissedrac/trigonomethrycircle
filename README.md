<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    canvas {
      border: 1px solid #000;
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

    // Function to draw grid background
    function drawGrid() {
      const gridSpacing = 10; // Spacing for grid cells
      ctx.beginPath();
      for (let x = 0; x <= canvas.width; x += gridSpacing) {
        ctx.moveTo(x, 0);
        ctx.lineTo(x, canvas.height);
      }
      for (let y = 0; y <= canvas.height; y += gridSpacing) {
        ctx.moveTo(0, y);
        ctx.lineTo(canvas.width, y);
      }
      ctx.strokeStyle = '#eaeaea'; // Light grey color for the grid lines
      ctx.stroke();
    }

    // Draw the unit circle
    function drawCircle() {
      ctx.beginPath();
      ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
      ctx.stroke();
    }

    // Clear previous point
    function clearCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawGrid();  // Draw grid background after clearing
      drawCircle();  // Redraw circle after clearing
    }

    // Draw a point on the circle at the given angle in radians
  function drawPoint() {
  let inputValue = document.getElementById('inputValue').value;
  // Заменяем символ π на выражение Math.PI и добавляем пробелы вокруг *, чтобы корректно выполнить операцию
  inputValue = inputValue.replace(/π/g, ' * Math.PI ');

  let angleInRadians = 0;
  if (inputValue.trim() !== '') {
    try {
      angleInRadians = eval(inputValue);
    } catch {
      alert("Invalid expression");
      return;
    }
  }

  // Здесь оставляем ваш остальной код для рисования точки...

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
