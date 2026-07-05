<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div class="relative min-h-screen w-full bg-[#363635] overflow-hidden">
	<div
		class="absolute inset-0 bg-center bg-no-repeat bg-contain opacity-25 pointer-events-none"
		style="background-image: url('/pyramid.gif'); background-size: 45%;"
	></div>

	<div class="relative z-10 w-full min-h-screen">
		{@render children()}
	</div>
</div>
