<script>
  import { onMount } from 'svelte';

  const questions = [
    {
      id: 1,
      question: 'What is the capital of France?',
      options: ['Paris', 'London', 'Madrid', 'Rome'],
      correctAnswer: 'Paris',
      userAnswer: null
    },
    {
      id: 2,
      question: 'Which planet is known as the Red Planet?',
      options: ['Venus', 'Mars', 'Mercury', 'Jupiter'],
      correctAnswer: 'Mars',
      userAnswer: null
    },
    {
      id: 3,
      question: 'Who painted the Mona Lisa?',
      options: ['Pablo Picasso', 'Leonardo da Vinci', 'Vincent van Gogh', 'Michelangelo'],
      correctAnswer: 'Leonardo da Vinci',
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
