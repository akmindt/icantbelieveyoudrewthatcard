<script>
  import {
    Button,
    Card,
    Heading,
    Hr,
    Input,
    Label,
    P,
  } from 'flowbite-svelte'

  let max = 1000
  let player1 = ""
  let player2 = ""
  let currentPlayer = ""
  
  function setPlayers() {

    // @ts-ignore
    player1 = document.getElementById("player1_input").value
    // @ts-ignore
    player2 = document.getElementById("player2_input").value
    // @ts-ignore
    max = document.getElementById("max_input").value

    currentPlayer = Math.floor(Math.random() * 2) + 1 == 1 ? player1 : player2
  }

  function roll() {
    max = Math.floor(Math.random() * max) + 1
    if (max > 1) {
      currentPlayer = currentPlayer == player1 ? player2 : player1
    }
  }

  function doubleOrNothing() {
    max = 1000
    currentPlayer = Math.floor(Math.random() * 2) + 1 == 1 ? player1 : player2
  }

  function reset() {
    max = 1000
    player1 = ""
    player2 = ""
  }
</script>

<svelte:head>
  <title>Gamba</title>
</svelte:head>

<Card size="lg" padding="xl">
  <Heading tag="h2" class="p-4">1v1 Credit Card Game</Heading>
  <P class="p-4">Roll for <s>raid loot</s> paying the bill!</P>
  <Hr classHr="my-8" />
  {#if !player1 && !player2}
    <form>
      <div class="grid gap-6 mb-6 md:grid-cols-2">
        <div>
          <Label for="player1_input" class="mb-2">Player 1</Label>
          <Input type="text" id="player1_input" placeholder="Sungjin" required />
        </div>
        <div>
          <Label for="player2_input" class="mb-2">Player 2</Label>
          <Input type="text" id="player2_input" placeholder="Mike" required />
        </div>
        <div>
          <Label for="max_input" class="mb-2">Max Roll</Label>
          <Input type="text" id="max_input" value="1000" required />
        </div>
      </div>
      <Button type="submit" on:click={setPlayers}>Submit</Button>
    </form>
  {:else if max > 1}
    <P>It is {currentPlayer}'s turn</P>
    <P>Current maximum: {max}</P>
    <Hr classHr="my-8" />
    <div class="grid gap-6 mb-6 md:grid-cols-2 w-1/2">
      <Button on:click={roll}>Roll</Button>
    </div>
  {:else}
    <P>Current maximum: {max}</P>
    <P>{currentPlayer} loses!</P>
    <Hr classHr="my-8" />
    <div class="grid gap-6 mb-6 md:grid-cols-2">
      <Button on:click={doubleOrNothing}>Double or nothing!</Button>
      <Button on:click={reset}>Reset</Button>
    </div>
  {/if}

  
</Card>

