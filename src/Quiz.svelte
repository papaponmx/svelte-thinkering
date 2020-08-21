<script>
  import Question from './Question.svelte';

  let quiz = getQuiz();
  let activeQuestion = 0;
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
</script>

<div>
  <button on:click={handleClick}>Start New Quiz</button>

  <h3>My Score: {score}</h3>
  <h3>Question # {activeQuestion + 1}</h3>
  {#await quiz}
    Loading....
  {:then data}

    {#each data.results as question, index}
      {#if index === activeQuestion}
        <Question {question} />
      {/if}
    {/each}

  {/await}
</div>
