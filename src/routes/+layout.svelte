<script>
	import '../app.css';
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<title>Bhushan</title>
</svelte:head>

<div
	class="flex min-h-screen flex-col bg-white text-gray-900 transition-colors dark:bg-[#1e1e1e] dark:text-white"
>
	<div class="mx-auto w-full max-w-[800px] p-8">
		<Navbar />
		<main class="flex flex-grow flex-col items-center justify-center text-center">
			{@render children()}
		</main>
		<Footer />
	</div>
</div>
