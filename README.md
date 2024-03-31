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
        <div id="playerCar" class="car" style="background-image: url('https://www.google.com/search?client=ms-android-samsung-ss&sca_esv=2fa414b916555b62&sca_upv=1&sxsrf=ACQVn08yS7xEuwYgbMO5ffatA5jW7Qf1TA:1711866155593&q=%EC%9E%90%EB%8F%99%EC%B0%A8+%EC%9C%84%EC%97%90%EC%84%9C+%EB%B3%B8%EB%AA%A8%EC%8A%B5&uds=AMwkrPvNVLCVGNFESV01Ay3iEWk6j-VeY_Um-1Rcv1kaUN0uit3pSEy3GChbeoAkiRDu3UQnfWNeEuvr2CLDtmz4QSZoluhJSDtgCuPEvtFPCu3qKBTbAr3r9yQUzcDO8FS8UdE8AuqO8yT298-ptVW65hgar9XfkGpAxdqCuCs_qjRQeBaQj6vAVot04vc3tfUvYhwcU-xc4NV-04LT2msB3VXb5YZjkUAmUiA4p2PUiMOgOoU7u7gMS_r8cGnFADfa8lktWajUMxAQzDmmM4RY5oN3_x5qKQ&udm=2&prmd=isvnbmz&sa=X&ved=2ahUKEwipo-2w7p2FAxWRcvUHHQY6C4QQtKgLegQICxAB&biw=360&bih=647&dpr=3#vhid=IOvDlbtLL192aM&vssid=mosaic&ip=1')"></div>
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
