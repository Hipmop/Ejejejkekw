  <!-- 클라이언트 측 코드 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Popcat Clicker</title>
    <style>
        #popcat {
            width: 200px;
            height: 200px;
            background-color: yellow;
            border-radius: 50%;
            text-align: center;
            line-height: 200px;
            cursor: pointer;
            user-select: none;
        }
    </style>
</head>
<body>
    <div id="popcat" onclick="sendClickEvent()">Click Me!</div>
    
    <script>
        function sendClickEvent() {
            fetch('/click', {
                method: 'POST',
            });
        }
    </script>
</body>
</html>
