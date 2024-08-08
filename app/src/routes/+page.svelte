<script>
	import { Button, Hr, P, Textarea } from 'flowbite-svelte';
	import excusesJson from '$lib/assets/excuses.json';

	let numUsed = 0;
	let excuse = '';
	const excuses = Object.values(excusesJson)[0];

	function getExcuse() {
		const index = Math.floor(Math.random() * excuses.length);
		excuse = excuses[index].excuse;
		numUsed += 1;
	}
</script>
<svelte:head>
	<title>I Can't Believe You Drew That Card!</title>
</svelte:head>

<div class="mb-6 grid gap-6 md:grid-cols-1 w-4/5">
	<P class="p-4">Tell me what happened in your game and I will tell you exactly why you lost!</P>
	<Textarea rows="10">
		<div slot="footer" class="flex items-center justify-between">
			<Button on:click={getExcuse} class="mt-5">Submit</Button>
		</div>
	</Textarea>
	{#if excuse !== ''}
		<Hr hrClass="my-8" />
		<P class="p-4">{excuse}</P>
	{/if}
</div>
