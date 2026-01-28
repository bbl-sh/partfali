<script>
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';
	import { Moon, Sun, Menu, X } from 'lucide-svelte';
	import { toggleTheme } from '$lib/theme.js';

	const navLinks = [
		{ path: '/', label: 'Home' },
		{ path: '/projects', label: 'Projects' },
		{ path: '/certifications', label: 'Certifications' }
	];

	let mobileMenuOpen = $state(false);
	let currentPath = $state('/');

	$effect(() => {
		const unsubscribe = page.subscribe((p) => {
			currentPath = p.url.pathname;
		});
		return unsubscribe;
	});

	function handleClick(path, e) {
		e.preventDefault();
		mobileMenuOpen = false;
		goto(path);
	}

	const isActive = (path) => currentPath === path;

	let isDark = $state(false);

	$effect(() => {
		if (typeof window !== 'undefined') {
			const saved = localStorage.getItem('theme');
			const prefersDark = window.matchMedia?.('(prefers-color-scheme: dark)').matches;
			const shouldDark = saved ? saved === 'dark' : prefersDark;
			document.documentElement.classList.toggle('dark', shouldDark);
			isDark = shouldDark;
		}
	});

	function onToggleTheme() {
		toggleTheme();
		isDark = document.documentElement.classList.contains('dark');
	}

	function toggleMobileMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}

	function getNavLinkClasses(path) {
		const base = 'relative rounded-lg px-4 py-2 text-sm font-medium transition-all duration-200';
		if (isActive(path)) {
			return `${base} text-emerald-600 dark:text-emerald-400 bg-emerald-50 dark:bg-emerald-950`;
		}
		return `${base} text-gray-600 dark:text-gray-400 hover:text-gray-900 hover:bg-gray-100 dark:hover:text-white dark:hover:bg-gray-800`;
	}

	function getMobileNavLinkClasses(path) {
		const base = 'block rounded-lg px-4 py-3 text-base font-medium transition-all duration-200';
		if (isActive(path)) {
			return `${base} text-emerald-600 dark:text-emerald-400 bg-emerald-50 dark:bg-emerald-950`;
		}
		return `${base} text-gray-600 dark:text-gray-400 hover:text-gray-900 hover:bg-gray-100 dark:hover:text-white dark:hover:bg-gray-800`;
	}
</script>

<header
	class="sticky top-0 z-50 w-full border-b border-gray-200 bg-white backdrop-blur-lg transition-colors duration-300 dark:border-gray-800 dark:bg-neutral-900"
>
	<nav class="mx-auto flex max-w-4xl items-center justify-between px-4 py-4 sm:px-6 lg:px-8">
		<!-- Logo -->
		<a
			href="/"
			onclick={(e) => handleClick('/', e)}
			class="text-xl font-bold tracking-tight text-gray-900 transition-colors hover:text-emerald-600 dark:text-white dark:hover:text-emerald-400"
		>
			<span class="gradient-text">B</span>hushan
		</a>

		<!-- Desktop Navigation -->
		<div class="hidden items-center gap-1 md:flex">
			{#each navLinks as link}
				<a
					href={link.path}
					onclick={(e) => handleClick(link.path, e)}
					class={getNavLinkClasses(link.path)}
				>
					{link.label}
				</a>
			{/each}

			<div class="ml-2 h-6 w-px bg-gray-200 dark:bg-gray-700"></div>

			<button
				class="ml-2 inline-flex items-center justify-center rounded-lg p-2.5 text-gray-500 transition-all duration-200 hover:bg-gray-100 hover:text-gray-900 dark:text-gray-400 dark:hover:bg-gray-800 dark:hover:text-white"
				aria-label="Toggle theme"
				onclick={onToggleTheme}
			>
				{#if isDark}
					<Sun class="h-5 w-5" />
				{:else}
					<Moon class="h-5 w-5" />
				{/if}
			</button>
		</div>

		<!-- Mobile Menu Button -->
		<div class="flex items-center gap-2 md:hidden">
			<button
				class="inline-flex items-center justify-center rounded-lg p-2.5 text-gray-500 transition-all duration-200 hover:bg-gray-100 hover:text-gray-900 dark:text-gray-400 dark:hover:bg-gray-800 dark:hover:text-white"
				aria-label="Toggle theme"
				onclick={onToggleTheme}
			>
				{#if isDark}
					<Sun class="h-5 w-5" />
				{:else}
					<Moon class="h-5 w-5" />
				{/if}
			</button>

			<button
				class="inline-flex items-center justify-center rounded-lg p-2.5 text-gray-500 transition-all duration-200 hover:bg-gray-100 hover:text-gray-900 dark:text-gray-400 dark:hover:bg-gray-800 dark:hover:text-white"
				aria-label="Toggle menu"
				onclick={toggleMobileMenu}
			>
				{#if mobileMenuOpen}
					<X class="h-5 w-5" />
				{:else}
					<Menu class="h-5 w-5" />
				{/if}
			</button>
		</div>
	</nav>

	<!-- Mobile Navigation -->
	{#if mobileMenuOpen}
		<div
			class="border-t border-gray-200 bg-white backdrop-blur-lg md:hidden dark:border-gray-800 dark:bg-neutral-900"
		>
			<div class="space-y-1 px-4 py-3">
				{#each navLinks as link}
					<a
						href={link.path}
						onclick={(e) => handleClick(link.path, e)}
						class={getMobileNavLinkClasses(link.path)}
					>
						{link.label}
					</a>
				{/each}
			</div>
		</div>
	{/if}
</header>
