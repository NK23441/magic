<script>
  import Team from "./Team.svelte";
  let blueScore = 5;
  let redScore =5;
  let winningText="";
  $: redWon = blueScore === 0;
  $: blueWon = redScore === 0;
  $: gameOver = redWon || blueWon;
  $: if (blueWon){
    winningText = "Blue Won!"
  } else{
    winningText = "Red Won!"
  }
  function newGame(){
    redScore = 5;
    blueScore =5;
  }
</script>
<div class="row">
  <div class="col">
    <h1 class="text-center">MTG COUNTER</h1>
  </div>
</div>
<div class="row">
  <Team {gameOver} team ="Red" bind:score ={redScore}/>
  <Team {gameOver} team = "Blue" bind:score={blueScore}/>
</div>
{#if !gameOver}
<div class="row mt-3">
  <div class="col">
    <button on:click={newGame} class="btn btn-warning w-100">Reset Game</button>
  </div>
</div>
{:else}
<div class="row mt-3">
  <div class="col">
    {#if blueWon}
    <h2 class="text-center text-primary">Blue Won</h2>
    {:else}
    <h2 class="text-center text-danger">Red Won</h2>
    {/if}
  </div>
</div>
<div class="row mt-3">
  <button on:click={newGame} class="btn btn-success w-100">New Game</button>
</div>
{/if}