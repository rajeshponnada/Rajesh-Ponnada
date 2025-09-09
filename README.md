# Rajesh-Ponnada

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>C Language Quiz</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {
      background-color: #f2f2f2;
      font-family: 'Segoe UI', sans-serif;
    }
    .quiz-container {
      max-width: 700px;
      margin: 60px auto;
      background: white;
      padding: 30px 40px;
      border-radius: 10px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
    }
    .question {
      font-size: 1.25rem;
      font-weight: 600;
    }
    .option-btn {
      margin: 10px 0;
      text-align: left;
    }
    .option-btn.correct {
      background-color: #28a745;
      color: white;
    }
    .option-btn.incorrect {
      background-color: #dc3545;
      color: white;
    }
    .score-section {
      font-size: 1.5rem;
      text-align: center;
    }
    .btn-restart {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h2 class="text-center mb-4">C Language Quiz</h2>
    <div id="quiz-box">
      <div id="question-container" class="mb-4">
        <div id="question" class="question">Loading...</div>
      </div>
      <div id="answer-buttons" class="d-grid gap-2"></div>
      <div class="mt-4 text-center">
        <button id="next-btn" class="btn btn-primary">Next</button>
      </div>
    </div>
    <div id="result-box" class="score-section d-none">
      <div id="score-text"></div>
      <button class="btn btn-success btn-restart" onclick="startQuiz()">Restart Quiz</button>
    </div>
  </div>

  <script>
    const questions = [
      {
        question: "Which of the following is a valid C variable name?",
        options: ["int", "float", "my_var", "double"],
        answer: "my_var"
      },
      {
        question: "What is the size of an int on a 32-bit system?",
        options: ["2 bytes", "4 bytes", "8 bytes", "Depends on compiler"],
        answer: "4 bytes"
      },
      {
        question: "Which header file is required for printf() function?",
        options: ["<conio.h>", "<string.h>", "<stdio.h>", "<stdlib.h>"],
        answer: "<stdio.h>"
      },
      {
        question: "Which loop is guaranteed to execute at least once?",
        options: ["for", "while", "do-while", "none"],
        answer: "do-while"
      },
      {
        question: "What is a pointer in C?",
        options: [
          "A variable that stores value",
          "A variable that stores address",
          "A keyword",
          "None of the above"
        ],
        answer: "A variable that stores address"
      },
      {
        question: "Which function is used to dynamically allocate memory in C?",
        options: ["alloc()", "malloc()", "calloc()", "memory()"],
        answer: "malloc()"
      },
      {
        question: "Which symbol is used for comments in C?",
        options: ["// or /* */", "#", "--", ";;"],
        answer: "// or /* */"
      },
      {
        question: "What is the correct way to declare a function in C?",
        options: [
          "function myFunc()",
          "void myFunc()",
          "declare myFunc()",
          "func myFunc()"
        ],
        answer: "void myFunc()"
      },
      {
        question: "Which keyword is used to exit a loop in C?",
        options: ["stop", "exit", "break", "return"],
        answer: "break"
      },
      {
        question: "What is the extension of a C source file?",
        options: [".cpp", ".c", ".cs", ".exe"],
        answer: ".c"
      }
    ];

    let currentQuestionIndex = 0;
    let score = 0;
    const questionElement = document.getElementById("question");
    const answerButtons = document.getElementById("answer-buttons");
    const nextButton = document.getElementById("next-btn");
    const resultBox = document.getElementById("result-box");
    const quizBox = document.getElementById("quiz-box");
    const scoreText = document.getElementById("score-text");

    function startQuiz() {
      currentQuestionIndex = 0;
      score = 0;
      quizBox.classList.remove("d-none");
      resultBox.classList.add("d-none");
      shuffleQuestions();
      showQuestion();
    }

    function shuffleQuestions() {
      questions.sort(() => Math.random() - 0.5);
    }

    function showQuestion() {
      resetState();
      const currentQuestion = questions[currentQuestionIndex];
      questionElement.textContent = currentQuestion.question;

      currentQuestion.options.forEach(option => {
        const button = document.createElement("button");
        button.textContent = option;
        button.classList.add("btn", "btn-outline-primary", "option-btn");
        answerButtons.appendChild(button);
        button.addEventListener("click", () => selectAnswer(button, currentQuestion.answer));
      });
    }

    function resetState() {
      nextButton.style.display = "none";
      answerButtons.innerHTML = "";
    }

    function selectAnswer(selectedBtn, correctAnswer) {
      const selectedAnswer = selectedBtn.textContent;
      const buttons = answerButtons.querySelectorAll("button");

      buttons.forEach(btn => {
        if (btn.textContent === correctAnswer) {
          btn.classList.add("correct");
        } else {
          btn.disabled = true;
        }
      });

      if (selectedAnswer === correctAnswer) {
        selectedBtn.classList.add("correct");
        score++;
      } else {
        selectedBtn.classList.add("incorrect");
      }

      nextButton.style.display = "block";
    }

    nextButton.addEventListener("click", () => {
      currentQuestionIndex++;
      if (currentQuestionIndex < questions.length) {
        showQuestion();
      } else {
        showScore();
      }
    });

    function showScore() {
      quizBox.classList.add("d-none");
      resultBox.classList.remove("d-none");

      scoreText.innerHTML = `
        You scored <strong>${score}</strong> out of <strong>${questions.length}</strong>.<br>
        ${score === questions.length ? "🏆 Perfect score!" :
          score >= 7 ? "🎉 Great job!" :
          score >= 5 ? "👍 Not bad!" :
          "📘 Keep practicing!"}
      `;
    }

    // Start quiz on first load
    startQuiz();
  </script>
</body>
</html>
