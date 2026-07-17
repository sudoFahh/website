<script lang="ts">
	import { page } from '$app/state';
</script>

{#if page.status === 404}
	<main class="min-h-screen flex flex-col items-center justify-center text-center p-4 text-white">
		<h1 class="text-2xl font-[Instrument_Serif] text-[#81E979]">404 (page not found)</h1>
		<a href="/" class="mt-7 link">go back home</a>
		<p class="text-[9px] font-[Jetbrains_Mono] mt-7">
			if you think this is a mistake, please <a href="mailto:m4.sh@tuta.io" class="link"
				>contact me</a
			>
		</p>
	</main>
{:else}
	<main class="min-h-screen flex flex-col items-center justify-center text-center p-4 text-white">
		<h1 class="text-2xl font-[Instrument_Serif] text-[#81E979]">
			{page.status}: {page.error?.message}
		</h1>
		<a href="/" class="mt-6 link">go back home</a>
		<p class="text-[9px] font-[Jetbrains_Mono] mt-6">
			if you think this is a mistake, please <a href="mailto:m4.sh@tuta.io" class="link"
				>contact me</a
			>
		</p>
	</main>
{/if}
