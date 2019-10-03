<script>
  export let question;

  let answers = question.incorrect_answers.map(answer => {
    return {
      answer,
      correct: false
    };
  });
  let allAnswers = [
    ...answers,
    {
      answer: question.correct_answer,
      correct: true
    }
  ];
  let isCorrect;
  let isAnswered = false;

  shuffle(allAnswers);

  function shuffle(arr) {
    arr.sort(() => Math.random() - 0.5);
  }

  function checkAnswer(correct) {
    isAnswered = true;
    isCorrect = correct;
  }
</script>

<h2>
  {@html question.question}
</h2>
{#if isAnswered}
  <h3>{isCorrect ? 'Correct!' : 'Wrong!'}</h3>
{/if}
{#each allAnswers as answer}
  <button on:click={() => checkAnswer(answer.correct)}>
    {@html answer.answer}
  </button>
{/each}
