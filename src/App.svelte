<script>
  import { onMount } from 'svelte';

  const questions = [
    {
      id: 1,
      question: 'Who is the first player to score a century in IPL?',
      options: ['Mccllumm', 'Raina', 'Kohli', 'Rohit'],
      correctAnswer: 'Mccllumm',
      selectedAnswer: ''
    },
    {
      id: 2,
      question: 'Which team has largest fan base in IPL?',
      options: ['MI', 'CSK', 'RCB', 'SRH'],
      correctAnswer: 'CSK',
      selectedAnswer: ''
    },
    {
      id: 3,
      question: 'Who is the fastest player to reach 1000 runs in IPL?',
      options: ['Kohli', 'Raina', 'Gayle', 'Gaikwad'],
      correctAnswer: 'Gaikwad',
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
