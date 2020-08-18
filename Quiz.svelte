<script>
  export let quizName = "Jaime's Quizz";
  let title;
  let a, b;
</script>
<div>
	<h2>{quizName}</h2>
  <h4>{title}</h4>
  <input bind:value={title} type="text">
  <input bind:value={a} type="number">
  <input bind:value={b} type="number">
  <h4>{a + b}  </h4>
  
</div>