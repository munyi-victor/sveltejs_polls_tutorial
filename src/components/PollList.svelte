<script>
  // import { onDestroy } from "svelte";
  import {fade, slide, scale} from "svelte/transition";
  import {flip} from "svelte/animate";
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
    {#each $PollStore as poll (poll.id)}
      <div in:fade out:scale|local animate:flip={{duration:500}}>
        <PollDetails {poll} />
      </div>
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