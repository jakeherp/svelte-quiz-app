<script>
  let result;
  let correctAnswer = "c";
  let answers = ["a", "b", "c", "d"];

  const pickAnswer = answer => {
    if (answer === correctAnswer) {
      return (result = "You win!");
    }
    return (result = "You lose!");
  };
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
