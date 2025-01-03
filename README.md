# data-structure-using-c-Rahulyadav12345678
data-structure-using-c-Rahulyadav12345678 created by GitHub Classroom
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IQ Calculator</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
    text-align: center;
}

.hidden {
    display: none;
}

button {
    padding: 10px 20px;
    background-color: #28a745;
    border: none;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
}

button:hover {
    background-color: #218838;
}

    </style>
</head>
<body>
    <div class="container">
        <h1>IQ Calculator</h1>
        <div id="question-container">
            <p id="question"></p>
            <div id="answer-options"></div>
            <button id="next-btn" onclick="nextQuestion()">Next</button>
        </div>
        <div id="result-container" class="hidden">
            <h2>Your IQ Score: <span id="iq-score"></span></h2>
            <button onclick="restartQuiz()">Retake Quiz</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>



///Java script code
const questions = [
    {
        question: "What comes next in the series: 1, 2, 4, 8, ...?",
        answers: [12, 16, 10, 20],
        correct: 1
    },
    {
        question: "Which shape does not belong in this sequence?",
        answers: ["Circle", "Square", "Triangle", "Pentagon"],
        correct: 2
    },
    {
        question: "What is 25 * 4?",
        answers: [100, 120, 150, 80],
        correct: 0
    },
    {
        question: "Which number is the smallest?",
        answers: [1, 0.5, -1, 0.1],
        correct: 2
    }
];

let currentQuestionIndex = 0;
let score = 0;

const questionElement = document.getElementById('question');
const answerOptionsElement = document.getElementById('answer-options');
const nextButton = document.getElementById('next-btn');
const iqScoreElement = document.getElementById('iq-score');
const questionContainer = document.getElementById('question-container');
const resultContainer = document.getElementById('result-container');

function showQuestion() {
    const currentQuestion = questions[currentQuestionIndex];
    questionElement.innerText = currentQuestion.question;
    answerOptionsElement.innerHTML = '';

    currentQuestion.answers.forEach((answer, index) => {
        const button = document.createElement('button');
        button.classList.add('answer-btn');
        button.innerText = answer;
        button.onclick = () => selectAnswer(index, currentQuestion.correct);
        answerOptionsElement.appendChild(button);
    });
}

function selectAnswer(selectedIndex, correctIndex) {
    if (selectedIndex === correctIndex) {
        score++;
    }
    nextQuestion();
}

function nextQuestion() {
    currentQuestionIndex++;
    if (currentQuestionIndex < questions.length) {
        showQuestion();
    } else {
        showResults();
    }
}

function showResults() {
    questionContainer.classList.add('hidden');
    resultContainer.classList.remove('hidden');
    const iqScore = Math.round((score / questions.length) * 150);
    iqScoreElement.innerText = iqScore;
}

function restartQuiz() {
    score = 0;
    currentQuestionIndex = 0;
    questionContainer.classList.remove('hidden');
    resultContainer.classList.add('hidden');
    showQuestion();
}

showQuestion();

