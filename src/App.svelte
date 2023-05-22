<script>
  import { onMount } from 'svelte';

  // Define the quiz questions and answers
  const quizQuestions = [
    {
      question: 'What is the capital of France?',
      answers: ['Paris', 'Madrid', 'London', 'Rome'],
      correctAnswer: 'Paris',
      userAnswer: null
    },
    {
      question: 'Who painted the Mona Lisa?',
      answers: ['Leonardo da Vinci', 'Pablo Picasso', 'Vincent van Gogh', 'Claude Monet'],
      correctAnswer: 'Leonardo da Vinci',
      userAnswer: null
    },
    // Add more questions here...
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
{/if}
