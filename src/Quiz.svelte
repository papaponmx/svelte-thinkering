<script>
  import { fly } from 'svelte/transition';
  import Question from './Question.svelte';
  import Modal from './Modal.svelte';

  let activeQuestion = 0;
  let isModalOpen = false;
  let quiz = getQuiz();
  let score = 0;

  async function getQuiz() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=10&category=12&type=multiple',
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }

  function nextQuestion() {
    ++activeQuestion;
  }

  const resetQuiz = () => {
    isModalOpen = false;
    score = 0;
    quiz = getQuiz();
  };

  const addToScore = () => {
    ++score;
  };

  $: if (score > 7) {
    isModalOpen = true;
  }

  $: questionNumber = activeQuestion + 1;
</script>

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>

<div>
  <button on:click={resetQuiz}>Start New Quiz</button>

  <h3>My Score: {score}</h3>
  <h3>Question # {questionNumber}</h3>
  {#await quiz}
    Loading....
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fade-wrapper">
          <Question {addToScore} {nextQuestion} {question} />
        </div>
      {/if}
    {/each}
  {/await}
</div>
{#if isModalOpen}
  <Modal on:CLOSE_MODAL={resetQuiz}>
    <h2>You Won!</h2>
    <p>Congratulations</p>
    <button on:click={resetQuiz}>Start over</button>
  </Modal>
{/if}
