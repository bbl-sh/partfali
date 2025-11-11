<script>
	import { goto } from '$app/navigation';
	import { Moon, Sun } from 'lucide-svelte';
	import { toggleTheme } from '$lib/theme.js';
	const navLinks = [
		{ path: '/', label: 'home' },
		{ path: '/projects', label: 'projects' },
		{ path: '/certifications', label: 'certifications' }
	];

	function handleClick(path, e) {
		e.preventDefault();
		goto(path);
	}

	// Active state without $page
	const isActive = (path) => typeof window !== 'undefined' && window.location.pathname === path;

	// Theme state + functions (no $page needed)
	let isDark = false;

	if (typeof window !== 'undefined') {
		const saved = localStorage.getItem('theme');
		const prefersDark = window.matchMedia?.('(prefers-color-scheme: dark)').matches;
		const shouldDark = saved ? saved === 'dark' : prefersDark;
		document.documentElement.classList.toggle('dark', shouldDark);
		isDark = shouldDark;
	}

	function onToggleTheme() {
		toggleTheme();
		// sync local state with DOM after toggling
		isDark = document.documentElement.classList.contains('dark');
	}
</script>

<nav class="mb-1 flex w-full items-center justify-center gap-4 overflow-x-auto p-4 md:gap-10">
	{#each navLinks as link}
		<a
			href={link.path}
			onclick={(e) => handleClick(link.path, e)}
			class="cursor-pointer no-underline transition-all duration-300 ease-in-out"
			class:text-gray-900={isActive(link.path)}
			class:dark:text-white={isActive(link.path)}
			class:font-semibold={isActive(link.path)}
			class:text-gray-500={!isActive(link.path)}
			class:dark:text-gray-400={!isActive(link.path)}
			class:hover:text-gray-900={!isActive(link.path)}
			class:hover:dark:text-white={!isActive(link.path)}
			class:hover:scale-105={!isActive(link.path)}
		>
			{link.label}
		</a>
	{/each}

	<button
		class="ml-2 inline-flex items-center rounded-md border border-gray-300 p-2
			text-gray-700 transition
			hover:bg-gray-100 dark:border-gray-700 dark:text-gray-200
			dark:hover:bg-gray-900/60"
		aria-label="Toggle theme"
		onclick={onToggleTheme}
	>
		{#if isDark}
			<Sun class="h-5 w-5" />
		{:else}
			<Moon class="h-5 w-5" />
		{/if}
	</button>
</nav>
