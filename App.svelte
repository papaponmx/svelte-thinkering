<script>
  import Button from './Button.svelte';
  import Quiz from './Quiz.svelte';
  let name = 'Jaime';
</script>

<style>
  main {
    font-family: sans-serif;
  }
</style>

<main>
	<Quiz quizName='My quizz' />
</main>