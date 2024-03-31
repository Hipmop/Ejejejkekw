
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
            width: 100px;
            height: 100px;
            background-size: cover;
            bottom: 0;
            transition: left 0.1s linear, top 0.1s linear;
        }
        #playerCar {
            left: 50%;
            transform: translateX(-50%);
        }
        .aiCar {
            background-color: transparent;
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <div id="playerCar" class="car" style="background-image: url('player_car.jpg')"></div>
    </div>
    <button onclick="changeDirection()">Change Direction</button>

    <script>
        const gameContainer = document.getElementById("gameContainer");
        const playerCar = document.getElementById("playerCar");

        const trackWidth = gameContainer.offsetWidth;
        const trackHeight = gameContainer.offsetHeight;
        const carWidth = playerCar.offsetWidth;
        const carHeight = playerCar.offsetHeight;

        let playerSpeed = 0;
        let aiSpeed = 5;
        let aiCars = [];

        // 플레이어 레이싱 카 이동
        function movePlayerCar(direction) {
            const currentLeft = parseInt(playerCar.style.left) || trackWidth / 2;
            if (direction === "left") {
                playerSpeed -= 0.5;
            } else if (direction === "right") {
                playerSpeed += 0.5;
            }
            playerSpeed *= 0.9; // 감속도
            const newLeft = currentLeft + playerSpeed;
            if (newLeft >= 0 && newLeft + carWidth <= trackWidth) {
                playerCar.style.left = newLeft + "px";
            }
        }

        // AI 레이싱 카 생성
        function createAICars() {
            const numberOfAICars = 5;
            for (let i = 0; i < numberOfAICars; i++) {
                const aiCar = document.createElement("div");
                aiCar.className = "car aiCar";
                aiCar.style.left = Math.random() * (trackWidth - carWidth) + "px";
                aiCar.style.backgroundImage = "url('ai_car.jpg')";
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

                // 충돌 감지
                if (checkCollision(playerCar, aiCar)) {
                    aiSpeed = 0;
                    setTimeout(() => {
                        aiSpeed = 5;
                    }, 1000);
                }
            });
        }

        // 충돌 감지 함수
        function checkCollision(car1, car2) {
            const rect1 = car1.getBoundingClientRect();
            const rect2 = car2.getBoundingClientRect();
            return !(rect1.right < rect2.left || 
                    rect1.left > rect2.right || 
                    rect1.bottom < rect2.top || 
                    rect1.top > rect2.bottom);
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

        // 방향 변경 버튼 클릭 이벤트 처리
        function changeDirection() {
            playerSpeed *= -1;
        }

        // 게임 루프
        setInterval(() => {
            moveAICars();
        }, 100);
    </script>
</body>
</html>
