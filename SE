<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joystick Game</title>
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
            y: canvas.height / 2,
            size: 20,
            speed: 3,
            dx: 0,
            dy: 0,

            draw: function() {
                ctx.fillStyle = "blue";
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            },

            update: function() {
                this.x += this.dx;
                this.y += this.dy;

                // 화면을 벗어나지 않도록 제한
                if (this.x - this.size < 0) {
                    this.x = this.size;
                }
                if (this.x + this.size > canvas.width) {
                    this.x = canvas.width - this.size;
                }
                if (this.y - this.size < 0) {
                    this.y = this.size;
                }
                if (this.y + this.size > canvas.height) {
                    this.y = canvas.height - this.size;
                }
            }
        };

        // 조이스틱 컨트롤러 이벤트 처리
        canvas.addEventListener("mousemove", function(event) {
            const rect = canvas.getBoundingClientRect();
            const scaleX = canvas.width / rect.width;
            const scaleY = canvas.height / rect.height;
            const mouseX = (event.clientX - rect.left) * scaleX;
            const mouseY = (event.clientY - rect.top) * scaleY;

            // 플레이어를 조이스틱 위치로 이동
            const angle = Math.atan2(mouseY - player.y, mouseX - player.x);
            player.dx = Math.cos(angle) * player.speed;
            player.dy = Math.sin(angle) * player.speed;
        });

        canvas.addEventListener("mouseleave", function() {
            // 마우스가 화면을 벗어나면 플레이어를 정지
            player.dx = 0;
            player.dy = 0;
        });

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            player.draw();
            player.update();

            requestAnimationFrame(gameLoop);
        }

        gameLoop();
    </script>
</body>
</html>
