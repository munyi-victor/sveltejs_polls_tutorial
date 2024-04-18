<script>
  import { onDestroy } from "svelte";
  import PollStore from "../store/PollStore";
  import PollDetails from "./PollDetails.svelte";

  // export let polls = [];

  // const unsub = PollStore.subscribe((data) => {
  //   polls = data;
  // })

  // onDestroy(() => {
  //   unsub();
  // })
</script>

{#if $PollStore.length > 0}
  <div class="poll-list">
    {#each $PollStore as poll}
      <PollDetails {poll} on:vote />
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