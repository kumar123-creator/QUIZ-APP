<script>
  import { onMount } from 'svelte';

  // Define the quiz questions and answers
  const quizQuestions = [
    {
      question: 'Who has scored the first century in IPL?',
      answers: ['Mccllumm', 'Raina', 'Kohli', 'Rohit'],
      correctAnswer: 'Mccllumm',
      userAnswer: null
    },
    {
      question: 'Which team has the largest fan base in IPL?',
      answers: ['KKR', 'CSK', 'RCB', 'MI'],
      correctAnswer: 'CSK',
      userAnswer: null
    },
   {
      question: 'Who has taken most wickets in an IPL season?',
      answers: ['Bravo', 'Bumrah', 'Malinga', 'Chahal'],
      correctAnswer: 'Bravo',
      userAnswer: null
    },
  ];

  let currentQuestionIndex = 0;
  let score = 0;

  function selectAnswer(answer) {
    quizQuestions[currentQuestionIndex].userAnswer = answer;
  }

  function nextQuestion() {
    if (quizQuestions[currentQuestionIndex].userAnswer === quizQuestions[currentQuestionIndex].correctAnswer) {
      score++;
    }

    currentQuestionIndex++;
  }

  // Calculate the user's score at the end of the quiz
  function calculateScore() {
    score = 0;

    quizQuestions.forEach(question => {
      if (question.userAnswer === question.correctAnswer) {
        score++;
      }
    });
  }

  // Optional: Initialize quiz data or perform other actions on mount
  onMount(() => {
    // Initialize quiz data if needed
  });
</script>

<style>
  /* Add CSS styles for the quiz app */
</style>

{#if currentQuestionIndex < quizQuestions.length}
  <div>
    <h2>Question {currentQuestionIndex + 1}</h2>
    <p>{quizQuestions[currentQuestionIndex].question}</p>

    <ul>
      {#each quizQuestions[currentQuestionIndex].answers as answer}
        <li>
          <label>
            <input type="radio" bind:group={quizQuestions[currentQuestionIndex].userAnswer} value={answer} on:change={() => selectAnswer(answer)} />
            {answer}
          </label>
        </li>
      {/each}
    </ul>

    <button on:click={nextQuestion}>Next</button>
  </div>
{:else}
  <div>
    <h2>Quiz Complete!</h2>
    <p>Your score: {score}/{quizQuestions.length}</p>

    <button on:click={calculateScore}>Try Again</button>
  </div>
{/if}<
