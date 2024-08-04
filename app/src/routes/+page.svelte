<script>
	import { Button, Card, Heading, Hr, P, Textarea } from 'flowbite-svelte';
	import excusesJson from '$lib/assets/excuses.json';

	let numUsed = 0;
	let excuse = '';
	let realityCheck = false;
	const realityCheckMsg =
		'Look at some point you need to realize that you absolutely had some amout of control over the outcome of the game. Seriously, it is time to get a grip and stop searching for any excuse and start looking at what you did in the game and if there was truly nothing else you could do, just accept variance and move on.';
	const excuses = Object.values(excusesJson)[0];
	const numExcuses = Math.ceil(Math.random() * 10);

	function getExcuse() {
		if (numUsed >= numExcuses) {
			realityCheck = true;
		} else {
			const index = Math.floor(Math.random() * excuses.length);
			excuse = excuses[index].value;
			numUsed += 1;
		}
	}
</script>

<div class="mb-6 grid gap-6 md:grid-cols-1">
	<Card size="xl" padding="xl">
		{#if realityCheck}
			<Heading tag="h1">{realityCheckMsg}</Heading>
		{:else}
			<P class="p-4">Tell me what happened in your game and I will tell you exactly what went wrong.</P>
			<Textarea rows="10">
				<div slot="footer" class="flex items-center justify-between">
					<Button on:click={getExcuse} class="mt-5">Submit</Button>
				</div>
			</Textarea>
			{#if excuse !== ''}
				<Hr hrClass="my-8" />
				<P>{excuse}</P>
			{/if}
		{/if}
	</Card>
</div>
