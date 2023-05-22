<script>
  import { onMount } from 'svelte';

  let questions = [
    {
      question: 'What is the capital of France?',
      options: ['Paris', 'London', 'Berlin', 'Madrid'],
      correctAnswer: 'Paris',
      selectedAnswer: null
    },
    {
      question: 'Who painted the Mona Lisa?',
      options: ['Leonardo da Vinci', 'Pablo Picasso', 'Vincent van Gogh', 'Michelangelo'],
      correctAnswer: 'Leonardo da Vinci',
      selectedAnswer: null
    },
    {
      question: 'What is the largest planet in our solar system?',
      options: ['Jupiter', 'Saturn', 'Mars', 'Earth'],
      correctAnswer: 'Jupiter',
      selectedAnswer: null
    }
  ];

  let currentQuestion = 0;
  let score = 0;

  function selectAnswer(answer) {
    questions[currentQuestion].selectedAnswer = answer;
  }

  function nextQuestion() {
    if (questions[currentQuestion].selectedAnswer === null) {
      alert('Please select an answer before proceeding.');
      return;
    }

    if (currentQuestion < questions.length - 1) {
      currentQuestion++;
    } else {
      calculateScore();
    }
  }

  function calculateScore() {
    score = questions.reduce((totalScore, question) => {
      if (question.selectedAnswer === question.correctAnswer) {
        return totalScore + 1;
      } else {
        return totalScore;
      }
    }, 0);
  }

  // Optional: Initialize quiz or perform other actions on mount
  onMount(() => {
    // Initialize quiz if needed
  });
</script>

<style>
  /* Add CSS styling for the quiz app */
</style>

{#if currentQuestion < questions.length}
  <div>
    <h2>{questions[currentQuestion].question}</h2>
    <ul>
      {#each questions[currentQuestion].options as option}
        <li>
          <label>
            <input type="radio" name="answer" value={option} on:change={() => selectAnswer(option)} />
            {option}
          </label>
        </li>
      {/each}
    </ul>
    <button on:click={nextQuestion}>Next</button>
  </div>
{:else}
  <div>
    <h2>Quiz completed!</h2>
    <p>Your score: {score}/{questions.length}</p>
  </div>
{/if}
