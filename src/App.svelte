<script>
  let questions = [
    {
      id: 1,
      question: "What is the capital of France?",
      options: ["Paris", "London", "Berlin"],
      correctAnswer: "Paris",
      selectedAnswer: ""
    },
    {
      id: 2,
      question: "Who painted the Mona Lisa?",
      options: ["Leonardo da Vinci", "Pablo Picasso", "Vincent van Gogh"],
      correctAnswer: "Leonardo da Vinci",
      selectedAnswer: ""
    },
    {
      id: 3,
      question: "What is the largest planet in our solar system?",
      options: ["Jupiter", "Saturn", "Mars"],
      correctAnswer: "Jupiter",
      selectedAnswer: ""
    }
  ];

  let currentQuestionIndex = 0;
  let score = 0;

  function selectAnswer(answer) {
    questions[currentQuestionIndex].selectedAnswer = answer;
  }

  function nextQuestion() {
    if (questions[currentQuestionIndex].selectedAnswer === "") {
      // Do not proceed if the user hasn't selected an answer
      return;
    }

    if (currentQuestionIndex < questions.length - 1) {
      currentQuestionIndex++;
    } else {
      // Quiz finished, calculate score
      score = calculateScore();
    }
  }

  function calculateScore() {
    let correctAnswers = 0;
    for (const question of questions) {
      if (question.selectedAnswer === question.correctAnswer) {
        correctAnswers++;
      }
    }
    return correctAnswers;
  }

  function resetQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    for (const question of questions) {
      question.selectedAnswer = "";
    }
  }
</script>

<style>
  /* Add CSS styles for the quiz app */
</style>

{#if currentQuestionIndex < questions.length}
  <div>
    <h3>Question {currentQuestionIndex + 1}</h3>
    <p>{questions[currentQuestionIndex].question}</p>

    <ul>
      {#each questions[currentQuestionIndex].options as option}
        <li>
          <label>
            <input type="radio" name="answer" bind:group={questions[currentQuestionIndex].selectedAnswer} value={option} on:change={() => selectAnswer(option)} />
            {option}
          </label>
        </li>
      {/each}
    </ul>

    <button on:click={nextQuestion}>Next</button>
  </div>
{:else}
  <div>
    <h3>Quiz Finished!</h3>
    <p>Your score: {score} out of {questions.length}</p>
    <button on:click={resetQuiz}>Restart Quiz</button>
  </div>
{/if}
