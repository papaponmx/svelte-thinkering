<script>
  export let quizName = "Jaime's Quizz";
  const correctAnswer = 'a';
  let result;
  let answers = ['a', 'b', 'c', 'd'];

  const pickAnswer = answer => {
    if (answer === correctAnswer) {
      return (result = 'CORRECT !');
    }
    return (result = 'NOOOOOOOO');
  };
</script>
<div>
	<h2>{quizName}</h2>
  {#if result}
    <h3>{result}</h3>
  {:else}
  <h3>Please pick an answer</h3>
  {/if}

  {#each answers as answer}
  <button on:click={() => pickAnswer(answer)}>{answer.toUpperCase()}</button>
  {/each}
</div>