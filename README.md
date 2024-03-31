<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird</title>
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

        const birdImage = new Image(); // 새 이미지 객체 생성
        birdImage.src = 'bird.png'; // 이미지 URL 설정

        const bird = {
            x: 50,
            y: canvas.height / 2,
            radius: 20,
            velocityY: 0,
            gravity: 0.03,
            jumpStrength: -1.5,

            jump: function() {
                this.velocityY = this.jumpStrength;
            },

            update: function() {
                this.velocityY += this.gravity;
                this.y += this.velocityY;

                if (this.y > canvas.height || this.y < 0) {
                    reset();
                }
            },

            draw: function() {
                ctx.drawImage(birdImage, this.x - this.radius, this.y - this.radius, this.radius * 2, this.radius * 2); // 이미지로 공 그리기
            }
        };

        // 다른 플레이어 추가
        const otherPlayers = [];

        function drawOtherPlayers() {
            otherPlayers.forEach(player => {
                ctx.drawImage(birdImage, player.x - player.radius, player.y - player.radius, player.radius * 2, player.radius * 2);
            });
        }

        function addOtherPlayer(x, y) {
            otherPlayers.push({x, y, radius: 20});
        }

        document.addEventListener("touchstart", function(event) {
            bird.jump();
        });

        function reset() {
            bird.y = canvas.height / 2;
            bird.velocityY = 0;
            pipes.length = 0;
            score = 0;
        }

        function collisionDetection() {
            pipes.forEach(p => {
                if (bird.x + bird.radius > p.x && bird.x - bird.radius < p.x + pipe.width &&
                    (bird.y - bird.radius < p.height || bird.y + bird.radius > p.height + pipe.gap)) {
                    reset();
                }
            });
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            bird.update();
            bird.draw();
            pipe.update();
            pipes.forEach(p => pipe.draw(p.x, p.height));
            collisionDetection();

            pipes.forEach(p => {
                if (p.x + pipe.width < bird.x && !p.passed) {
                    score++;
                    p.passed = true;
                }
            });

            drawScore();
            drawOtherPlayers(); // 다른 플레이어 그리기

            requestAnimationFrame(gameLoop);
        }

        function drawScore() {
            ctx.fillStyle = "black";
            ctx.font = "20px Arial";
            ctx.fillText("Score: " + score, 10, 30);
        }

        // 다른 플레이어 추가
        addOtherPlayer(150, canvas.height / 2);
        addOtherPlayer(250, canvas.height / 3);

        gameLoop();
    </script>
</body>
</html>
