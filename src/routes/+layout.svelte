<script>
	import '../app.css';
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<title>Bhushan | Software Developer</title>
	<meta name="description" content="Bhushan's portfolio - MLOps, AI Agents, LLMs, and DevOps" />
</svelte:head>

<div
	class="flex min-h-screen flex-col bg-gradient-to-b from-gray-50 to-white text-gray-900 transition-colors duration-300 dark:from-neutral-900 dark:to-neutral-950 dark:text-white"
>
	<Navbar />
	<main class="mx-auto w-full max-w-4xl flex-grow px-4 py-2 sm:px-6 lg:px-8">
		{@render children()}
	</main>
	<Footer />
</div>
