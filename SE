<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rhythm Game</title>
    <style>
        canvas {
            border: 1px solid black;
            display: block;
            margin: 0 auto;
            touch-action: manipulation; /* 모바일에서 기본 스크롤 이벤트 막기 */
        }
    </style>
</head>
<body>
    <canvas id="canvas" width="480" height="320"></canvas>
    <script>
        const canvas = document.getElementById("canvas");
        const ctx = canvas.getContext("2d");

        const keyboardKeys = ['a', 's', 'd', 'f']; // 건반에 해당하는 키
        const keyColors = ['red', 'green', 'blue', 'yellow']; // 건반 색상

        const notes = []; // 리듬 노트 배열
        const noteSpeed = 2; // 노트 이동 속도
        const noteSize = 40; // 노트 크기
        const noteSpawnProbability = 0.05; // 노트 생성 확률
        const scoreDecreaseRate = 0.1; // 노트를 놓칠 때 점수가 감소하는 비율

        let score = 0; // 점수 변수
        let isGameOver = false; // 게임 종료 여부

        // 사용자 입력 처리
        canvas.addEventListener('touchstart', function(event) {
            event.preventDefault(); // 기본 터치 동작 막기
            if (!isGameOver) {
                const touchX = event.touches[0].clientX;
                const touchIndex = Math.floor((touchX / canvas.clientWidth) * keyboardKeys.length);
                checkNoteHit(touchIndex);
            } else {
                resetGame();
            }
        });

        // 노트 객체 생성 함수
        function createNote() {
            const randomKeyIndex = Math.floor(Math.random() * keyboardKeys.length);
            const randomX = Math.random() * (canvas.width - noteSize);
            const note = {
                x: randomX,
                y: -noteSize,
                keyIndex: randomKeyIndex
            };
            notes.push(note);
        }

        // 노트 이동 및 그리기 함수
        function moveAndDrawNotes() {
            notes.forEach(note => {
                note.y += noteSpeed;
                ctx.fillStyle = keyColors[note.keyIndex];
                ctx.fillRect(note.x, note.y, noteSize, noteSize);
            });
        }

        // 노트와 건반의 충돌 체크 함수
        function checkNoteHit(keyIndex) {
            const hitNoteIndex = notes.findIndex(note => note.keyIndex === keyIndex && note.y >= canvas.height - noteSize);
            if (hitNoteIndex !== -1) {
                notes.splice(hitNoteIndex, 1);
                score++;
            } else {
                score -= scoreDecreaseRate;
                if (score < 0) {
                    score = 0;
                }
            }
        }

        // 게임 오버 처리 함수
        function gameOver() {
            isGameOver = true;
            alert(`Game Over! Your score: ${score}. Tap to restart.`);
        }

        // 게임 초기화 함수
        function resetGame() {
            notes.length = 0;
            score = 0;
            isGameOver = false;
        }

        // 게임 루프
        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            if (!isGameOver) {
                if (Math.random() < noteSpawnProbability) { // 일정 확률로 노트 생성
                    createNote();
                }
                moveAndDrawNotes();
            }

            // 점수 표시
            ctx.fillStyle = 'black';
            ctx.font = '20px Arial';
            ctx.fillText('Score: ' + Math.round(score), 10, 30); // 반올림하여 정수로 표시

            requestAnimationFrame(gameLoop);
        }

        gameLoop();
    </script>
</body>
</html>
