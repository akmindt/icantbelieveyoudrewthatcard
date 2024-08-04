<script lang="ts">
	import '../app.postcss';
	import { page } from '$app/stores';
	import {
		Footer,
		FooterBrand,
		FooterCopyright,
		FooterIcon,
		FooterLink,
		FooterLinkGroup,
		Img,
		Navbar,
		NavLi,
		NavUl,
		NavHamburger
	} from 'flowbite-svelte';
	import Logo from '/favicon-32x32.png';
	$: activeUrl = $page.url.pathname;
	
</script>

<div class="min-h-screen">
<header class="w-full mx-auto bg-white dark:bg-slate-950">
	<Navbar class="px-2 sm:px-4 py-2.5 w-full z-20 top-0 start-0 border-b" color="form">
		I Can't Believe You Drew That Card!
		<NavHamburger />
		<NavUl {activeUrl}>
			<NavLi href="/">Home</NavLi>
			<NavLi href="/hypergeocalc">Hyper Geo Calc</NavLi>
			<NavLi href="https://twitter.com/akmindt">Twitter</NavLi>
			<NavLi href="https://ko-fi.com/akmindt">Leave a Tip!</NavLi>
		</NavUl>
	</Navbar>
</header>
	<main class="flex justify-center items-center pt-20">
		<slot />
	</main>
<footer class="sticky top-[100vh] px-4 mx-auto">
	<Footer>
		<div class="sm:flex sm:items-center sm:justify-between">
			<FooterCopyright href="/" by="Aaron Mindt" year={2024} />
		</div>
	</Footer>
</footer>
</div>