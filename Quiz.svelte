<script>
  export let quizName = "Jaime's Quizz";
  const correctAnswer = 'a';
  let result;
  let answers = ['a', 'b', 'c', 'd'];
  let quiz;

  async function getQuiz() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=10&category=12&difficulty=easy&type=multiple',
    );
    const quiz = res.json();
  }

  const pickAnswer = answer => {
    if (answer === correctAnswer) {
      return (result = 'CORRECT !');
    }
    return (result = 'NOOOOOOOO');
  };
</script>
<div>
	<h2>{quizName}</h2>

  <button on:click={() => getQuiz()}>Get Quiz</button>
  {#if quiz}
   <h3>{quiz.result[0].question}</h3>
  {/if}

  {#if result}
    <h3>{result}</h3>
  {:else}
  <h3>Please pick an answer</h3>
  {/if}

  {#each answers as answer}
  <button on:click={() => pickAnswer(answer)}>{answer.toUpperCase()}</button>
  {/each}
</div>