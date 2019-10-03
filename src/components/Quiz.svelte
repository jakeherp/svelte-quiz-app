<script>
  let result;
  let correctAnswer = "c";
  let answers = ["a", "b", "c", "d"];
  let quiz = getQuiz();

  const pickAnswer = answer => {
    if (answer === correctAnswer) {
      return (result = "You win!");
    }
    return (result = "You lose!");
  };

  async function getQuiz() {
    const res = await fetch(
      `https://opentdb.com/api.php?amount=10&category=22&difficulty=medium&type=multiple`
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<style>
  .lose {
    color: tomato;
  }
  .win {
    color: forestgreen;
  }
</style>

<div>
  {#await quiz}
    Loading ...
  {:then data}
    <h3>{data.results[0].question}</h3>
  {/await}

  <button on:click={handleClick}>Start quiz</button>
  {#if result}
    <h2 class={result === 'You win!' ? 'win' : 'lose'}>{result}</h2>
  {:else}
    <h2>Please answer the question</h2>
  {/if}

  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>
      Answer {answer.toUpperCase()}
    </button>
  {/each}
</div>
