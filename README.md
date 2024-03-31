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
        
        const player = {
            x: canvas.width / 2,
            y: canvas.height - 30,
            width: 20,
            height: 20,
            color: '#00ff00',
            speed: 5,
            leftPressed: false,
            rightPressed: false
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

        function drawPlayer() {
            ctx.beginPath();
            ctx.rect(player.x, player.y, player.width, player.height);
            ctx.fillStyle = player.color;
            ctx.fill();
            ctx.closePath();
        }

        function updatePlayerPosition() {
            if (player.leftPressed && player.x > 0) {
                player.x -= player.speed;
            } else if (player.rightPressed && player.x < canvas.width - player.width) {
                player.x += player.speed;
            }
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawPlayer();
            updatePlayerPosition();
            requestAnimationFrame(draw);
        }

        draw();
    </script>
</body>
</html>
