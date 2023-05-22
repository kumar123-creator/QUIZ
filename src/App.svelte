<script>
  import { onMount } from 'svelte';

  const questions = [
    {
      id: 1,
      question: 'Who has scored the first century in IPL?',
      options: ['Mccllumm', 'Raina', 'Kohli', 'Rohit'],
      correctAnswer: 'Mccllumm',
      userAnswer: null
    },
    {
      id: 2,
      question: 'Which team has the largest fan base in IPL?',
      options: ['KKR', 'CSK', 'RCB', 'MI'],
      correctAnswer: 'CSK',
      userAnswer: null
    },
    {
      id: 3,
      question: 'Who has taken most wickets in an IPL season?',
      options: ['Bravo', 'Bumrah', 'Malinga', 'Chahal'],
      correctAnswer: 'Bravo',
      userAnswer: null
    }
    // Add more questions here...
  ];

  let currentQuestionIndex = 0;
  let score = 0;
  let quizCompleted = false;

  function selectAnswer(answer) {
    questions[currentQuestionIndex].userAnswer = answer;
  }

  function nextQuestion() {
    currentQuestionIndex++;

    if (currentQuestionIndex === questions.length) {
      // Quiz completed
      quizCompleted = true;
      calculateScore();
    }
  }

  function calculateScore() {
    score = questions.reduce((totalScore, question) => {
      if (question.userAnswer === question.correctAnswer) {
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
  /* Add Bootstrap or Tailwind CSS classes for styling */
</style>

{#if !quizCompleted}
  <div>
    <h2>Question {currentQuestionIndex + 1}</h2>
    <p>{questions[currentQuestionIndex].question}</p>
    <ul>
      {#each questions[currentQuestionIndex].options as option}
        <li>
          <label>
            <input
              type="radio"
              name="answer"
              value={option}
              on:change={() => selectAnswer(option)}
              disabled={questions[currentQuestionIndex].userAnswer !== null}
            />
            {option}
          </label>
        </li>
      {/each}
    </ul>
    {#if questions[currentQuestionIndex].userAnswer !== null}
      <p>Your answer: {questions[currentQuestionIndex].userAnswer}</p>
    {/if}
    <button on:click={nextQuestion} disabled={questions[currentQuestionIndex].userAnswer === null}>Next</button>
  </div>
{:else}
  <div>
    <h2>Quiz completed</h2>
    <p>Your score: {score}/{questions.length}</p>
  </div>
{/if}
