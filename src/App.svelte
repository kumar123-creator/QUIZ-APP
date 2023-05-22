<script>
  let questions = [
    {
      "question": "Which of the following special symbol allowed in a variable name?",
      "options": [
        "* (asterisk)",
        "| (pipeline)",
        "- (hyphen)",
        "_ (underscore)"
      ],
      "correctIndex": 3
    },
    {
      "question": "Which of the following correctly shows the hierarchy of arithmetic operations in C?",
      "options": [
        "/ + * -",
        "* - / +",
        "+ - / *",
        "/ * + -"
      ],
      "correctIndex": 3
    },
    {
      "question": "Which header file should be included to use functions like malloc() and calloc()?",
      "options": [
        "memory.h",
        "stdlib.h",
        "string.h",
        "dos.h"
      ],
      "correctIndex": 1
    },
    {
      "question": "Which bitwise operator is suitable for turning off a particular bit in a number?",
      "options": [
        "&& operator",
        "& operator",
        "|| operator",
        "! operator"
      ],
      "correctIndex": 1
    },
    {
      "question": "What function should be used to free the memory allocated by calloc() ?",
      "options": [
        "dealloc();",
        "malloc(variable_name, 0)",
        "free();",
        "memalloc(variable_name, 0)"
      ],
      "correctIndex": 2
    }
  ];
  let answers = new Array(questions.length).fill(null);
  let questionPointer = -1;

  function getScore() {
    let score = answers.reduce((acc, val, index) => {
      if (questions[index].correctIndex === val) {
        return acc + 1;
      }
      return acc;
    }, 0);
    return (score / questions.length * 100) + "%";
  }

  function restartQuiz() {
    answers = new Array(questions.length).fill(null);
    questionPointer = 0;
  }
</script>

<style>
  /* Add your styles here */
</style>

<div class="app">
  {#if questionPointer === -1}
    <div class="start-screen">
      <button on:click={() => { questionPointer = 0 }}>
        Start Quiz
      </button>
    </div>
  {:else if !(questionPointer > answers.length - 1)}
    <div class="quiz-screen">
      <div class="main">
        <h2>
          {questions[questionPointer].question}
        </h2>
        <div class="options">
          {#each questions[questionPointer].options as opt, i}
            <button class="{answers[questionPointer] === i ? 'selected' : ''}" on:click={() => { answers[questionPointer] = i }}>
              {opt}
            </button>
          {/each}
        </div>
      </div>
      <div class="footer">
        <div class="progress-bar">
          <div style="width: {questionPointer / questions.length * 100}%"></div>
        </div>
        <div class="buttons">
          <button disabled={questionPointer === 0} on:click={() => { questionPointer-- }}>
            &lt;
          </button>
          <button disabled={answers[questionPointer] === null} on:click={() => { questionPointer++ }}>
            &gt;
          </button>
        </div>
      </div>
    </div>
  {:else}
   <div class="score-screen">
			<h1>
				Your score: {getScore()}
			</h1>
			<button on:click={restartQuiz}>
				Restart Quiz
			</button>
		</div>
	{/if}
</div>
