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
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    color: #333;
}

.quiz-container {
    background: white;
    padding: 30px;
    border-radius: 15px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    width: 100%;
    max-width: 450px;
    text-align: center;
}

h1 {
    color: #4a5568;
    margin-top: 0;
}

.stats {
    font-size: 1.1rem;
    font-weight: bold;
    margin-bottom: 20px;
    color: #4c51bf;
}

#question-box {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 25px;
    padding: 15px;
    background-color: #f7fafc;
    border-radius: 10px;
    border: 2px dashed #cbd5e0;
}

.options-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
    margin-bottom: 20px;
}

.option-btn {
    background-color: #edf2f7;
    border: 2px solid #e2e8f0;
    padding: 15px;
    font-size: 1.2rem;
    font-weight: 600;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s ease;
}

.option-btn:hover {
    background-color: #e2e8f0;
    transform: translateY(-2px);
}

.option-btn:active {
    transform: translateY(0);
}

/* Màu sắc khi đúng/sai */
.correct {
    background-color: #48bb78 !important;
    color: white;
    border-color: #38a169;
}

.wrong {
    background-color: #f56565 !important;
    color: white;
    border-color: #e53e3e;
}

.feedback {
    font-size: 1.2rem;
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 15px;
}

.feedback.correct-text { color: #38a169; }
.feedback.wrong-text { color: #e53e3e; }

#next-btn {
    background-color: #4c51bf;
    color: white;
    border: none;
    padding: 12px 25px;
    font-size: 1rem;
    font-weight: bold;
    border-radius: 8px;
    cursor: pointer;
    width: 100%;
}

#next-btn:hover {
    background-color: #434190;
}

.hidden {
    display: none !important;
}
let score = 0;
let correctAnswer = 0;
let hasAnswered = false;

// Lấy các phần tử giao diện
const questionBox = document.getElementById('question-box');
const optionsBox = document.getElementById('options-box');
const scoreBoard = document.getElementById('score-board');
const feedback = document.getElementById('feedback');
const nextBtn = document.getElementById('next-btn');

// Hàm tạo số ngẫu nhiên trong khoảng [min, max]
function getRandomNumber(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Hàm tự động sinh câu hỏi và bộ đáp án
function generateQuestion() {
    hasAnswered = false;
    feedback.classList.add('hidden');
    nextBtn.classList.add('hidden');
    optionsBox.innerHTML = ''; // Xóa các nút cũ

    // 1. Sinh ngẫu nhiên phép tính
    const num1 = getRandomNumber(1, 20);
    const num2 = getRandomNumber(1, 20);
    const operators = ['+', '-', '*'];
    const selectedOperator = operators[getRandomNumber(0, operators.length - 1)];

    // 2. Tính toán đáp án đúng
    if (selectedOperator === '+') {
        correctAnswer = num1 + num2;
    } else if (selectedOperator === '-') {
        correctAnswer = num1 - num2;
    } else {
        correctAnswer = num1 * num2;
    }

    // Hiển thị câu hỏi lên màn hình
    // Thay đổi dấu '*' thành 'x' cho thân thiện với người dùng
    const displayOperator = selectedOperator === '*' ? 'x' : selectedOperator;
    questionBox.innerText = `${num1} ${displayOperator} ${num2} = ?`;

    // 3. Tự động sinh ra 3 đáp án sai (bẫy) xung quanh đáp án đúng
    let answersSet = new Set();
    answersSet.add(correctAnswer); // Đưa đáp án đúng vào trước

    while (answersSet.size < 4) {
        // Sinh đáp án sai lệch trong khoảng từ -10 đến +10 so với đáp án đúng
        let wrongAns = correctAnswer + getRandomNumber(-10, 10);
        if (wrongAns !== correctAnswer) {
            answersSet.add(wrongAns);
        }
    }

    // Chuyển Set thành mảng và trộn ngẫu nhiên vị trí các đáp án
    const answersArray = Array.from(answersSet).sort(() => Math.random() - 0.5);

    // 4. Tạo các nút bấm hiển thị đáp án
    answersArray.forEach(ans => {
        const button = document.createElement('button');
        button.innerText = ans;
        button.classList.add('option-btn');
        button.addEventListener('click', () => checkAnswer(button, ans));
        optionsBox.appendChild(button);
    });
}

// Hàm kiểm tra khi người dùng chọn đáp án
function checkAnswer(selectedButton, chosenAnswer) {
    if (hasAnswered) return; // Nếu đã bấm rồi thì không cho bấm lại
    hasAnswered = true;

    const allButtons = optionsBox.querySelectorAll('.option-btn');

    if (chosenAnswer === correctAnswer) {
        // Trả lời đúng
        selectedButton.classList.add('correct');
        score += 10;
        scoreBoard.innerText = `Điểm: ${score}`;
        feedback.innerText = "Chính xác! 🎉";
        feedback.className = "feedback correct-text";
    } else {
        // Trả lời sai
        selectedButton.classList.add('wrong');
        feedback.innerText = `Sai rồi! Đáp án đúng là: ${correctAnswer}`;
        feedback.className = "feedback wrong-text";

        // Tìm và làm nổi bật nút chứa đáp án đúng lên cho người chơi thấy
        allButtons.forEach(btn => {
            if (parseInt(btn.innerText) === correctAnswer) {
                btn.classList.add('correct');
            }
        });
    }

    // Hiện nút để qua câu tiếp theo
    nextBtn.classList.remove('hidden');
}

// Bắt sự kiện nút "Câu tiếp theo"
nextBtn.addEventListener('click', generateQuestion);

// Chạy game lần đầu tiên khi tải trang
generateQuestion();
