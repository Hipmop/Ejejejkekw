<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Racing Game</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            font-family: Arial, sans-serif;
        }
        canvas {
            display: block;
            background-color: #333;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="600"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');

        const playerCar = new Image();
        playerCar.src = 'player_car.png';
        const aiCar = new Image();
        aiCar.src = 'ai_car.png';

        const player = {
            x: canvas.width / 2,
            y: canvas.height - 50,
            width: 50,
            height: 50,
            speed: 5,
            leftPressed: false,
            rightPressed: false,
            image: playerCar
        };

        const ai = {
            x: Math.random() * (canvas.width - 50),
            y: -50,
            width: 50,
            height: 50,
            speed: 5,
            image: aiCar
        };

        document.addEventListener('keydown', keyDownHandler);
        document.addEventListener('keyup', keyUpHandler);

        function keyDownHandler(event) {
            if (event.key === 'Left' || event.key === 'ArrowLeft') {
                player.leftPressed = true;
            } else if (event.key === 'Right' || event.key === 'ArrowRight') {
                player.rightPressed = true;
            }
        }

        function keyUpHandler(event) {
            if (event.key === 'Left' || event.key === 'ArrowLeft') {
                player.leftPressed = false;
            } else if (event.key === 'Right' || event.key === 'ArrowRight') {
                player.rightPressed = false;
            }
        }

        function drawCar(car) {
            ctx.drawImage(car.image, car.x, car.y, car.width, car.height);
        }

        function updatePlayerPosition() {
            if (player.leftPressed && player.x > 0) {
                player.x -= player.speed;
            } else if (player.rightPressed && player.x < canvas.width - player.width) {
                player.x += player.speed;
            }
        }

        function updateAIPosition() {
            ai.y += ai.speed;
            if (ai.y > canvas.height) {
                ai.x = Math.random() * (canvas.width - ai.width);
                ai.y = -50;
            }
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawCar(player);
            drawCar(ai);
            updatePlayerPosition();
            updateAIPosition();
            requestAnimationFrame(draw);
        }

        draw();
    </script>
</body>
</html>
