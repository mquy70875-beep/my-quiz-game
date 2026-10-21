# my-quiz-game<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Đố Vui Toán Học Ngẫu Nhiên</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="quiz-container">
        <h1>Thử Thách Toán Học 🧠</h1>
        <div class="stats">
            <span id="score-board">Điểm: 0</span>
        </div>
        
        <div id="question-box">Đang tải câu hỏi...</div>
        
        <div class="options-container" id="options-box">
            <!-- Các nút đáp án sẽ tự động sinh ra ở đây -->
        </div>
        
        <div id="feedback" class="feedback hidden"></div>
        <button id="next-btn" class="hidden">Câu tiếp theo ➡️</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
