<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Popcorn Site</title>
    <style>
        #movies {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            padding: 20px;
        }
        .movie {
            width: 200px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            text-align: center;
            cursor: pointer;
        }
        .movie img {
            width: 100%;
            border-radius: 5px;
        }
        .movie h2 {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div id="movies">
        <div class="movie" onclick="replaceImage(this)">
            <img src="https://via.placeholder.com/150" alt="Movie">
            <h2>Movie Title 1</h2>
        </div>
        <div class="movie" onclick="replaceImage(this)">
            <img src="https://via.placeholder.com/150" alt="Movie">
            <h2>Movie Title 2</h2>
        </div>
        <div class="movie" onclick="replaceImage(this)">
            <img src="https://via.placeholder.com/150" alt="Movie">
            <h2>Movie Title 3</h2>
        </div>
        <!-- 여기에 추가 영화 정보를 계속해서 추가할 수 있습니다 -->
    </div>
    
    <!-- 소리를 재생할 오디오 객체 -->
    <audio id="popcornSound" src="popcorn.mp3"></audio>

    <script>
        function replaceImage(element) {
            // 클릭된 이미지의 src 속성을 변경합니다.
            element.querySelector("img").src = "new_image_url.jpg"; // 새로운 이미지 URL로 변경해주세요
        }
    </script>
</body>
</html>
