<script>
  let currentQuestion = 0;
  let score = 0;

  const questions = [
    {
      question: 'Question 1',
      options: ['Option 1', 'Option 2', 'Option 3'],
      correctAnswer: 0
    },
    {
      question: 'Question 2',
      options: ['Option 1', 'Option 2', 'Option 3'],
      correctAnswer: 1
    },
    {
      question: 'Question 3',
      options: ['Option 1', 'Option 2', 'Option 3'],
      correctAnswer: 2
    }
  ];

  function selectAnswer(event) {
    const selectedOption = event.target.value;
    const currentQuestionObj = questions[currentQuestion];

    if (parseInt(selectedOption) === currentQuestionObj.correctAnswer) {
      score++;
    }

    if (currentQuestion < questions.length - 1) {
      currentQuestion++;
    } else {
      // End of quiz
      alert('Quiz completed! Your score: ' + score);
    }
  }
</script>

<style>
  /* Add CSS styling for the quiz app */
</style>

<h1>Quiz App</h1>

{#if currentQuestion < questions.length}
  <div>
    <h2>{questions[currentQuestion].question}</h2>
    <ul>
      {#each questions[currentQuestion].options as option, index}
        <li>
          <label>
            <input
              type="radio"
              name="answer"
              value={index}
              on:change={selectAnswer}
            />
            {option}
          </label>
        </li>
      {/each}
    </ul>
  </div>
{:else}
  <p>Quiz completed! Your score: {score}</p>
{/if}
