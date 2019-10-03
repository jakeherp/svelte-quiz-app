<script>
  import Question from "./Question.svelte";

  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch(
      `https://opentdb.com/api.php?amount=15&category=22&difficulty=medium&type=multiple`
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<div>
  {#await quiz}
    Loading ...
  {:then data}
    {#each data.results as question}
      <Question {question} />
    {/each}
  {/await}

  <button on:click={handleClick}>Start quiz</button>

</div>
