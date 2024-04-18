<script>
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];
</script>

{#if polls.length > 0}
  <div class="poll-list">
    {#each polls as poll}
      <PollDetails {poll} />
    {/each}
  </div>

{:else} 
  <div class="container">
    <p>No Polls Available</p>
  </div>
{/if}

<style>
  .poll-list {
    text-align: left;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  .container p{
    text-align: center;
  }
</style>