<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fly } from 'svelte/transition';

	const quotes = [
		'manik',
		'a goofy guy',
		'a student',
		'a.. what?',
		'a developer',
		'a neeeeeeeeeeeerd',
		'an exception(e)',
		'an alien'
	];

	let quote = $state(quotes[0]);
	let lastIndex = -1;
	let interval: ReturnType<typeof setInterval>;

	let canvas: HTMLCanvasElement;
	let matrixInterval: ReturnType<typeof setInterval>;
	let resizeHandler: () => void;

	onMount(() => {
		interval = setInterval(() => {
			let index;
			do {
				index = Math.floor(Math.random() * quotes.length);
			} while (index === lastIndex);

			lastIndex = index;
			quote = quotes[index];
		}, 4000);

		// matrix rain
		const ctx = canvas.getContext('2d')!;
		let width: number, height: number, drops: number[];
		const fontSize = 14;
		const chars = '01アイウエオカキクケコサシスセソ0123456789<>{}[]/;';

		function setup() {
			width = canvas.width = window.innerWidth;
			height = canvas.height = window.innerHeight;
			const columns = Math.floor(width / fontSize);
			drops = new Array(columns).fill(1);
		}
		setup();

		function draw() {
			ctx.fillStyle = 'rgba(242, 236, 206, 0.45)'; // matches bg color, fades old chars
			ctx.fillRect(0, 0, width, height);

			ctx.fillStyle = 'rgba(0, 0, 0, 0.25)'; // low-contrast chars
			ctx.font = `${fontSize}px 'JetBrains Mono', monospace`;
			for (let i = 0; i < drops.length; i++) {
				const char = chars[Math.floor(Math.random() * chars.length)];
				ctx.fillText(char, i * fontSize, drops[i] * fontSize);
				if (drops[i] * fontSize > height && Math.random() > 0.975) drops[i] = 0;
				drops[i]++;
			}
		}
		matrixInterval = setInterval(draw, 50);

		resizeHandler = () => setup();
		window.addEventListener('resize', resizeHandler);
	});

	onDestroy(() => {
		clearInterval(interval);
		clearInterval(matrixInterval);
		if (resizeHandler) window.removeEventListener('resize', resizeHandler);
	});
</script>

<main
	class="relative z-10 bg-[#f2ecce] min-h-screen flex flex-col items-center justify-center text-center p-4"
>
	<canvas bind:this={canvas} class="fixed inset-0 z-0 pointer-events-none"></canvas>
	<div class="relative z-10 flex flex-col items-center">
		<h2 class="text-xl">hi, im</h2>
		<span class="block mb-2 h-7 overflow-hidden">
			{#key quote}
				<h2 class="block text-2xl" transition:fly={{ x: 10, duration: 300 }}>
					{quote}
				</h2>
			{/key}
		</span>

		<div class="mx-auto text-left">
			<p>i do a lot of random stuff. im (currently) a 14 year old student.</p>
			<p class="text-xs">
				im part of schools tech club (well 2 of them), robonexus and tech syndicate
			</p>
		</div>

		<!-- deez are website links -->
		<div class="mt-6 flex gap-4">
			<a class="font-bold italic hover:underline" href="/">/</a>
			<a class="italic hover:underline" href="/about">/about</a>
			<a class="italic hover:underline" href="/blog">/blog</a>
			<a class="italic hover:underline" href="/projects">/projects</a>
			<a class="italic hover:underline" href="/webrings">sillies</a>
		</div>

		<!-- deez are other links -->
		<div class="mt-6 flex gap-4">
			<a class="italic hover:underline" href="https://github.com/sudofahh">github</a>
			<a class="italic hover:underline" href="https://www.youtube.com/@m4shing_sm4shing">yt</a>
			<a class="italic hover:underline" href="https://www.instagram.com/m4shing_sm4shing/">ig</a>
			<a class="italic hover:underline" href="https://www.linkedin.com/in/manik-sharma-30b4a9419/"
				>linkedin</a
			>
			<a class="italic hover:underline" href="https://vncl.xyz">""company"" website</a>
		</div>
		<p class="text-xs">my links are also available @ https://links.maniksharma.xyz</p>
	</div>
</main>
