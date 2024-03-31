<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Racing Game</title>
    <style>
        #playerCar {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 100px;
            background-color: red;
        }
        .aiCar {
            position: absolute;
            width: 50px;
            height: 100px;
            background-color: blue;
        }
    </style>
</head>
<body>
    <div id="playerCar"></div>
    <div id="aiCarsContainer"></div>

    <script>
        const playerCar = document.getElementById("playerCar");
        const aiCarsContainer = document.getElementById("aiCarsContainer");

        const playerSpeed = 5;
        const aiSpeed = 4;
        const trackWidth = window.innerWidth;
        const trackHeight = window.innerHeight;

        let playerPosition = trackWidth / 2;
        let aiCars = [];

        // 플레이어 레이싱 카 이동
        function movePlayerCar(direction) {
            if (direction === "left") {
                playerPosition -= playerSpeed;
                if (playerPosition < 0) playerPosition = 0;
            } else if (direction === "right") {
                playerPosition += playerSpeed;
                if (playerPosition > trackWidth) playerPosition = trackWidth;
            }
            playerCar.style.left = playerPosition + "px";
        }

        // AI 레이싱 카 생성
        function createAICars() {
            const numberOfAICars = 5;
            for (let i = 0; i < numberOfAICars; i++) {
                const aiCar = document.createElement("div");
                aiCar.className = "aiCar";
                aiCar.style.left = Math.floor(Math.random() * trackWidth) + "px";
                aiCarsContainer.appendChild(aiCar);
                aiCars.push(aiCar);
            }
        }

        // AI 레이싱 카 이동
        function moveAICars() {
            aiCars.forEach((aiCar) => {
                const currentLeft = parseInt(aiCar.style.left);
                const newLeft = currentLeft + aiSpeed;
                aiCar.style.left = newLeft + "px";

                if (newLeft > trackWidth) {
                    aiCar.style.left = "0px";
                }
            });
        }

        createAICars();

        // 키보드 입력 이벤트 처리
        document.addEventListener("keydown", (event) => {
            if (event.key === "ArrowLeft") {
                movePlayerCar("left");
            } else if (event.key === "ArrowRight") {
                movePlayerCar("right");
            }
        });

        // 게임 루프
        setInterval(() => {
            moveAICars();
        }, 100);
    </script>
</body>
</html>
