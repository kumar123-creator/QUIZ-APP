<script>
  import { onMount } from 'svelte';

  const questions = [
    {
      id: 1,
      question: 'What is the capital of France?',
      options: ['Paris', 'London', 'Berlin', 'Rome'],
      correctAnswer: 'Paris',
      selectedAnswer: null,
    },
    {
      id: 2,
      question: 'Which planet is known as the Red Planet?',
      options: ['Mars', 'Jupiter', 'Venus', 'Mercury'],
      correctAnswer: 'Mars',
      selectedAnswer: null,
    },
    {
      id: 3,
      question: 'Who painted the Mona Lisa?',
      options: ['Leonardo da Vinci', 'Pablo Picasso', 'Vincent van Gogh', 'Michelangelo'],
      correctAnswer: 'Leonardo da Vinci',
      selectedAnswer: null,
    },
  ];

  let score = 0;

  function selectAnswer(questionId, answer) {
    const question = questions.find((q) => q.id === questionId);
    question.selectedAnswer = answer;
  }

  function calculateScore() {
    score = questions.reduce((acc, question) => {
      return question.selectedAnswer === question.correctAnswer ? acc + 1 : acc;
    }, 0);
  }

  // Optional: Initialize data or perform other actions on mount
  onMount(() => {
    // Initialize data if needed
  });
</script>

<style>
  /* Add Bootstrap or Tailwind CSS classes for styling */
</style>

{#each questions as question}
  <div class="question">
    <h3>{question.question}</h3>
    <ul>
      {#each question.options as option}
        <li>
          <label>
            <input
              type="radio"
              name={`question-${question.id}`}
              value={option}
              bind:checked={question.selectedAnswer}
              on:change={() => selectAnswer(question.id, option)}
            />
            {option}
          </label>
        </li>
      {/each}
    </ul>
  </div>
{/each}

<button on:click={calculateScore}>Submit</button>

{#if score > 0}
  <p>Your score: {score} out of {questions.length}</p>
{/if}
