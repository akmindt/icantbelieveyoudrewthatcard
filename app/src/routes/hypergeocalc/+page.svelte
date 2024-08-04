<script>
  import {
    Button,
    Card,
    Heading,
    Hr,
    Input,
    Label,
    P,
  } from 'flowbite-svelte';

  let value = 0.0;

  function calculate() {
    const num = Math.floor(Math.random() * 10) + 1;
    const denom = Math.floor(Math.random() * 10) + 1;
    const decimals = Math.floor(Math.random() * 1000) + 1;

    value = (1 / decimals) * (num / denom);
  }

  
</script>

<Card size="lg" padding="xl">
  <div>

    <Heading tag="h2" class="p-4">Hyper Geometric Calculator</Heading>
    <P class="p-4">Enter values into the calculator to see just how unlucky you are!</P>
    <Hr classHr="my-8" />
    <form>
      <div class="grid gap-6 mb-6 md:grid-cols-2">
        <div>
          <Label for="population_size" class="mb-2">Population Size</Label>
          <Input type="text" id="population_size" placeholder="60" />
        </div>
        <div>
          <Label for="successes" class="mb-2">Number of Successes in Population</Label>
          <Input type="text" id="successes" placeholder="4" />
        </div>
        <div>
          <Label for="sample_size" class="mb-2">Sample Size</Label>
          <Input type="text" id="sample_size" placeholder="20" />
        </div>
        <div>
          <Label for="sample_success" class="mb-2">Number of Successes in Sample</Label>
          <Input type="text" id="sample_success" placeholder="4" />
        </div>
        <Button type="submit" on:click={calculate}>Submit</Button>
      </div>
    </form>
    
    {#if value !== 0.0}
    <P>{value}%</P>
    <P>Wow you're so unlucky!</P>
    {/if}
    
  </div>
</Card>

