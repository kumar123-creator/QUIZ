<script>
  let questions = [
    {
      "question": "Who has scored first century in IPL?",
      "options": [
        "Mccllumm",
        "Raina",
        "Kohli",
        "Rohit"
      ],
      "correctIndex": 0
    },
    {
      "question": "Which team has largest fan base in IPL?",
      "options": [
        "KKR",
        "CSK",
        "RCB",
        "MI"
      ],
      "correctIndex": 1
    },
    {
      "question": "Which team has won most IPL trophies?",
      "options": [
        "CSK",
        "KKR",
        "MI",
        "SRH"
      ],
      "correctIndex": 2
    },
    {
      "question": "Who has scored most centuries in IPL?",
      "options": [
        "Rohit",
        "Gayle",
        "Kohli",
        "Raina"
      ],
      "correctIndex": 1
    },
    {
      "question": "Who has taken most wickets in an IPL season ?",
      "options": [
        "Bumrah",
        "Chahal",
        "Bravo",
        "Malinga"
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
