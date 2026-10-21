# my-quiz-game
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Hỏi Đáp Của Tôi</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="game-box">
        <h1>TRÒ CHƠI ĐỐ VUI 🎉</h1>
        
        <!-- Khu vực hiển thị số câu hỏi và điểm số -->
        <div class="stats">
            <span id="question-number">Câu hỏi: 1/3</span>
            <span id="score">Điểm: 0</span>
        </div>

        <!-- Nội dung câu hỏi -->
        <div id="question-text">Đang tải câu hỏi...</div>

        <!-- Danh sách các nút bấm đáp án -->
        <div id="answer-buttons" class="btn-grid">
            <!-- Code JavaScript sẽ tự sinh các nút vào đây -->
        </div>

        <!-- Nút để chuyển sang câu tiếp theo -->
        <button id="next-btn" class="hide">Câu tiếp theo ➡️</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
