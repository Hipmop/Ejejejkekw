<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Infinite Stairs</title>
    <style>
        canvas {
            border: 1px solid black;
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <canvas id="canvas" width="480" height="320"></canvas>
    <script>
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        const player = {
            x: canvas.width / 2,
            y: canvas.height - 50,
            width: 50,
            height: 50,
            velocityY: 0,
            gravity: 0.5,
            jumpStrength: -10,

            jump: function() {
                if (this.y === canvas.height - this.height) {
                    this.velocityY = this.jumpStrength;
                }
            },

            update: function() {
                this.velocityY += this.gravity;
                this.y += this.velocityY;

                if (this.y > canvas.height - this.height) {
                    this.y = canvas.height - this.height;
                    this.velocityY = 0;
                }
            },

            draw: function() {
                ctx.fillStyle = "blue";
                ctx.fillRect(this.x, this.y, this.width, this.height);
            }
        };

        const stairs = [];

        const stair = {
            width: 100,
            height: 20,
            speed: 3,
            gap: 150,
            interval: 1000, // 새 계단 생성 간격
            lastStairTime: 0,

            update: function() {
                // 일정 시간마다 새 계단 생성
                if (Date.now() - this.lastStairTime > this.interval) {
                    const newX = Math.random() * (canvas.width - this.width);
                    stairs.push({ x: newX });
                    this.lastStairTime = Date.now();
                }

                // 계단 이동
                stairs.forEach(s => {
                    s.y += this.speed;
                });

                // 화면을 벗어난 계단 제거
                if (stairs.length > 0 && stairs[0].y > canvas.height) {
                    stairs.shift();
                }
            },

            draw: function() {
                ctx.fillStyle = "green";
                stairs.forEach(s => {
                    ctx.fillRect(s.x, s.y, this.width, this.height);
                });
            }
        };

        function collisionDetection() {
            stairs.forEach(s => {
                if (player.y + player.height > s.y && player.x + player.width > s.x && player.x < s.x + stair.width) {
                    player.y = s.y - player.height;
                }
            });
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            player.update();
            player.draw();
            stair.update();
            stair.draw();
            collisionDetection();

            requestAnimationFrame(gameLoop);
        }

        document.addEventListener("keydown", function(event) {
            if (event.code === "Space") {
                player.jump();
            }
        });

        gameLoop();
    </script>
</body>
</html>
