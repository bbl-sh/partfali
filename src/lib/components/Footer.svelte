<script>
	import { Github, Twitter, Linkedin, Heart } from 'lucide-svelte';

	const socialLinks = [
		{ href: 'https://github.com/john221wick', icon: Github, label: 'GitHub' },
		{ href: 'https://x.com/nu_b_kh', icon: Twitter, label: 'Twitter' },
		{
			href: 'https://www.linkedin.com/in/bhushan-bharat-51ba4825b/',
			icon: Linkedin,
			label: 'LinkedIn'
		}
	];

	const year = new Date().getFullYear();
</script>

<footer class="mt-auto border-t border-gray-200 bg-white dark:border-gray-800 dark:bg-neutral-950">
	<div class="mx-auto max-w-4xl px-4 py-8 sm:px-6 lg:px-8">
		<div class="flex flex-col items-center gap-6 sm:flex-row sm:items-center sm:justify-between">
			<!-- Social Links (minimal, no glow) -->
			<nav aria-label="Social links" class="flex items-center gap-3">
				{#each socialLinks as { href, icon: Icon, label }}
					<a
						{href}
						target="_blank"
						rel="noopener noreferrer"
						aria-label={label}
						class="inline-flex h-10 w-10 items-center justify-center rounded-lg border border-gray-200 text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:border-gray-800 dark:text-gray-400 dark:hover:bg-gray-900 dark:hover:text-white"
					>
						<Icon class="h-5 w-5" />
					</a>
				{/each}
			</nav>

			<!-- Copyright -->
			<p class="flex items-center gap-1.5 text-sm text-gray-500 dark:text-gray-500">
				<span>&copy; {year} Bhushan. Built with</span>
				<Heart class="h-4 w-4 text-red-500" />
			</p>
		</div>
	</div>
</footer>
