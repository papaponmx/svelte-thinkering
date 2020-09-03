<script>
  export let addToScore;
  export let nextQuestion;
  export let question;
  let isCorrect;
  let isAnswered = false;
  const answers = question.incorrect_answers.map((answer) => ({
    answer,
    correct: false,
  }));

  const allAnswers = [
    ...answers,
    {
      answer: question.correct_answer,
      correct: true,
    },
  ];

  const shuffle = (array) => {
    array.sort(() => Math.random() - 0.5);
  };

  const checkQuestion = (correct) => {
    isAnswered = true;
    isCorrect = correct;
    correct && addToScore();
  };

  shuffle(allAnswers);
</script>

<style>
  h4 {
    color: red;
  }

  h4.isCorrect {
    color: green;
  }
</style>

<h3>
  {@html question.question}
</h3>

{#if isAnswered}
  <h4 class:isCorrect>
    {#if isCorrect}You got it right{:else}You goofed up{/if}
  </h4>
{/if}

{#each allAnswers as answer}
  <button on:click|once={() => checkQuestion(answer.correct)}>
    {@html answer.answer}
  </button>
{/each}

{#if isAnswered}<button on:click={nextQuestion}>Next Question</button>{/if}
