<script>
  import { onMount } from 'svelte';

  const questions = [
    {
      id: 1,
      question: 'What is the capital of France?',
      options: ['Paris', 'Madrid', 'Rome', 'Berlin'],
      correctAnswer: 'Paris',
      selectedAnswer: ''
    },
    {
      id: 2,
      question: 'Which planet is known as the Red Planet?',
      options: ['Venus', 'Mars', 'Jupiter', 'Saturn'],
      correctAnswer: 'Mars',
      selectedAnswer: ''
    },
    {
      id: 3,
      question: 'What is the tallest mountain in the world?',
      options: ['Mount Everest', 'K2', 'Kangchenjunga', 'Makalu'],
      correctAnswer: 'Mount Everest',
      selectedAnswer: ''
    }
  ];

  let currentQuestionIndex = 0;
  let score = 0;

  function selectAnswer(answer) {
    questions[currentQuestionIndex].selectedAnswer = answer;
  }

  function nextQuestion() {
    if (currentQuestionIndex < questions.length - 1) {
      currentQuestionIndex++;
    } else {
      calculateScore();
    }
  }

  function calculateScore() {
    score = questions.reduce((totalScore, question) => {
      if (question.selectedAnswer === question.correctAnswer) {
        return totalScore + 1;
      }
      return totalScore;
    }, 0);
  }

  // Optional: Initialize quiz or perform other actions on mount
  onMount(() => {
    // Initialize quiz data if needed
  });
</script>

<style>
  /* Add Bootstrap or Tailwind CSS classes for styling */
</style>

{#if currentQuestionIndex < questions.length}
  <h2>Question {currentQuestionIndex + 1}</h2>
  <p>{questions[currentQuestionIndex].question}</p>

  <div>
    {#each questions[currentQuestionIndex].options as option}
      <label>
        <input type="radio" bind:group={questions[currentQuestionIndex].selectedAnswer} value={option} on:change={() => selectAnswer(option)} />
        {option}
      </label>
    {/each}
  </div>

  <button on:click={nextQuestion}>Next</button>
{:else}
  <h2>Quiz Completed</h2>
  <p>Your score: {score} out of {questions.length}</p>
{/if}
