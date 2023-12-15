<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Cobrinha</title>
    <style>
        canvas {
            border: 1px solid #000;
            display: block;
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <canvas id="snakeCanvas" width="400" height="400"></canvas>

    <script>
        const canvas = document.getElementById("snakeCanvas");
        const ctx = canvas.getContext("2d");

        const box = 20;
        let snake = [{x: 10, y: 10}];
        let direction = "right";

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            for (let i = 0; i < snake.length; i++) {
                ctx.fillStyle = i === 0 ? "#00F" : "#0F0";
                ctx.fillRect(snake[i].x * box, snake[i].y * box, box, box);

                ctx.strokeStyle = "#000";
                ctx.strokeRect(snake[i].x * box, snake[i].y * box, box, box);
            }
        }

        function update() {
            const headX = snake[0].x;
            const headY = snake[0].y;

            if (direction === "right") headX++;
            if (direction === "left") headX--;
            if (direction === "up") headY--;
            if (direction === "down") headY++;

            const newHead = { x: headX, y: headY };
            snake.unshift(newHead);
        }

        function gameLoop() {
            update();
            draw();
        }

        setInterval(gameLoop, 100);
    </script>
</body>
</html>
