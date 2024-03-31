<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Racing Game</title>
    <style>
        #gameContainer {
            position: relative;
            width: 800px;
            height: 600px;
            margin: 0 auto;
            overflow: hidden;
            border: 2px solid black;
        }
        .car {
            position: absolute;
            width: 50px;
            height: 100px;
            background-color: red;
            bottom: 0;
            transition: left 0.1s linear;
        }
        #playerCar {
            left: 50%;
            transform: translateX(-50%);
        }
        .aiCar {
            background-color: blue;
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <div id="playerCar" class="car"></div>
    </div>

    <script>
        const gameContainer = document.getElementById("gameContainer");
        const playerCar = document.getElementById("playerCar");

        const trackWidth = gameContainer.offsetWidth;
        const trackHeight = gameContainer.offsetHeight;
        const carWidth = playerCar.offsetWidth;
        const carHeight = playerCar.offsetHeight;

        let playerSpeed = 5;
        let aiSpeed = 4;
        let aiCars = [];

        // 플레이어 레이싱 카 이동
        function movePlayerCar(direction) {
            const currentLeft = parseInt(playerCar.style.left) || trackWidth / 2;
            if (direction === "left") {
                const newLeft = currentLeft - playerSpeed;
                if (newLeft >= 0) {
                    playerCar.style.left = newLeft + "px";
                }
            } else if (direction === "right") {
                const newLeft = currentLeft + playerSpeed;
                if (newLeft + carWidth <= trackWidth) {
                    playerCar.style.left = newLeft + "px";
                }
            }
        }

        // AI 레이싱 카 생성
        function createAICars() {
            const numberOfAICars = 5;
            for (let i = 0; i < numberOfAICars; i++) {
                const aiCar = document.createElement("div");
                aiCar.className = "car aiCar";
                aiCar.style.left = Math.random() * (trackWidth - carWidth) + "px";
                gameContainer.appendChild(aiCar);
                aiCars.push(aiCar);
            }
        }

        // AI 레이싱 카 이동
        function moveAICars() {
            aiCars.forEach((aiCar) => {
                const currentTop = parseInt(aiCar.style.top) || 0;
                const newTop = currentTop + aiSpeed;
                aiCar.style.top = newTop + "px";

                if (newTop > trackHeight) {
                    aiCar.style.top = "0px";
                    aiCar.style.left = Math.random() * (trackWidth - carWidth) + "px";
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
