// server.js
const express = require('express');
const app = express();
const path = require('path');

let clickCount = 0;

app.use(express.static(path.join(__dirname, 'public')));
app.use(express.json());

app.post('/click', (req, res) => {
    clickCount++;
    console.log(`Current Click Count: ${clickCount}`);
    res.sendStatus(200);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

// 클라이언트 측 스크립트
document.getElementById("popcat").addEventListener("click", () => {
    fetch('/click', {
        method: 'POST',
    });
});
