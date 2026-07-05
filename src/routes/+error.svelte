<script lang="ts">
	import { page } from '$app/state';
</script>

{#if page.status === 404}
	<main class="min-h-screen flex flex-col items-center justify-center text-center p-4 text-white">
		<h1 class="text-2xl font-[Instrument_Serif] text-[#81E979]">coming soon</h1>
		<a href="/" class="mt-6 italic hover:underline text-[#8FBB99] font-[Jetbrains_Mono]"
			>go back home</a
		>
	</main>
{:else}
	<p>{page.status}: {page.error?.message}</p>
{/if}
