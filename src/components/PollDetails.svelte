<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../shared/Card.svelte";

  export let poll;

  // reactive
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor(poll.votesA / totalVotes * 100);
  $: percentB = Math.floor(poll.votesB / totalVotes * 100);

  const dispatch = createEventDispatcher();

  const handlVote = (option, id) => {
    dispatch("vote", {option, id});
  }
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>

    <p>Total votes: {totalVotes}</p>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => handlVote("a", poll.id)}>
      <div class="percent percent-a" style="width: {percentA}%;"></div>
      <span>{poll.answerA} ({poll.votesA})</span>
    </div>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => handlVote("b", poll.id)}>
      <div class="percent percent-b" style="width: {percentB}%;"></div>
      <span>{poll.answerB} ({poll.votesB})</span>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }

  p{
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }

  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
    border-radius: 6px;
  }

  .answer:hover {
    opacity: 0.6;
  }

  span {
    display: inline-block;
    padding: 10px 20px;
  }

  .percent {
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }

  .percent-a {
    border-left: 3px solid rgba(217, 27, 66, 0.2);
    background: rgba(217, 27, 66, 0.2);
  }

  .percent-b{
    border-left: 3px solid rgba(69, 196, 150, 0.2);
    background: rgba(69, 196, 150, 0.2);
  }
</style>