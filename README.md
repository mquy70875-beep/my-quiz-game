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
/* Định dạng chung cho toàn bộ trang web */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f2f5;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

/* Khung chứa trò chơi nằm ở giữa màn hình */
.game-box {
    background: white;
    width: 100%;
    max-width: 500px;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    text-align: center;
}

/* Thanh hiển thị điểm và số thứ tự câu hỏi */
.stats {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    font-weight: bold;
    color: #555;
}

/* Định dạng chữ của câu hỏi */
#question-text {
    font-size: 1.4rem;
    margin-bottom: 25px;
    font-weight: bold;
}

/* Bố cục lưới xếp 2 cột cho các nút đáp án */
.btn-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
    margin-bottom: 20px;
}

/* Định dạng cơ bản cho các nút bấm đáp án */
.btn {
    background-color: #e4e6eb;
    border: none;
    padding: 15px;
    font-size: 1.1rem;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.2s;
}

.btn:hover {
    background-color: #d8dadf;
}

/* Màu sắc hiển thị khi bấm ĐÚNG hoặc SAI */
.correct {
    background-color: #2ed573 !important;
    color: white;
}

.wrong {
    background-color: #ff4757 !important;
    color: white;
}

/* Nút "Câu tiếp theo" */
#next-btn {
    background-color: #0084ff;
    color: white;
    border: none;
    padding: 12px;
    width: 100%;
    font-size: 1.1rem;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

#next-btn:hover {
    background-color: #006bce;
}

/* Lớp ẩn phần tử khi chưa cần thiết */
.hide {
    display: none;
}
