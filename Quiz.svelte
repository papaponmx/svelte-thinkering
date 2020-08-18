<script>
  export let quizName = "Jaime's Quizz";
  const correctAnswer = 'A';
  let result;

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
  <button on:click={() => pickAnswer('A')}>A</button>
  <button on:click={() => pickAnswer('B')}>B</button>
  <button on:click={() => pickAnswer('C')}>C</button>
  <button on:click={() => pickAnswer('D')}>D</button>

</div>