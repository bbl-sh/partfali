<script>
	import { fly } from 'svelte/transition';
	import {
		Github,
		ExternalLink,
		FolderGit2,
		Sparkles,
		Cpu,
		Server,
		Code2,
		Box,
		Layers
	} from 'lucide-svelte';

	const categories = [
		{ id: 'all', label: 'All', description: 'Everything in one view' },
		{
			id: 'build',
			label: 'Build from scratch',
			description: 'Learning by rebuilding core systems'
		},
		{ id: 'ai', label: 'AI projects', description: 'LLMs, agents, and ML systems' },
		{ id: 'devops', label: 'DevOps', description: 'CI/CD, IaC, and automation pipelines' },
		{ id: 'linux', label: 'Linux + kernels', description: 'Systems, kernels, and low-level work' },
		{ id: 'gpu', label: 'GPU', description: 'CUDA and accelerated computing' },
		{ id: 'ongoing', label: 'Ongoing', description: 'Active experiments and research' },
		{ id: 'finished', label: 'Finished', description: 'Shipped and wrapped up' },
		{ id: 'live', label: 'Live projects', description: 'Public demos you can try' }
	];

	let selectedCategory = 'all';
	let showFilters = false;

	let projectsOngoing = [
		{
			title: 'Agentic CI/CD',
			description:
				'Building intelligent CI/CD pipelines with AI agents for automated testing and deployment',
			href: 'https://github.com/john221wick/agentic-ci-cd',
			demoHref: null,
			icon: Sparkles,
			tags: ['AI', 'DevOps', 'Automation'],
			categories: ['ai', 'ongoing', 'build', 'devops']
		},
		{
			title: 'Making miniGPT',
			description:
				'Building a GPT model from scratch to understand transformer architecture deeply',
			href: 'https://github.com/john221wick/building-llm',
			demoHref: 'https://building-llm.vercel.app/',
			icon: Cpu,
			tags: ['LLM', 'Deep Learning', 'Python'],
			categories: ['ai', 'build', 'live', 'ongoing']
		},
		{
			title: 'Leetcode Clone',
			description:
				'A competitive programming platform with code execution and problem solving features',
			href: 'https://github.com/john221wick/cp-platform',
			demoHref: 'https://cp-platform-one.vercel.app/',
			icon: Code2,
			tags: ['Full Stack', 'Svelte 5', 'Node.js'],
			categories: ['build', 'live', 'finished']
		},
		{
			title: 'GPU Programming',
			description: 'Exploring CUDA and GPU computing for high-performance parallel processing',
			href: 'https://github.com/john221wick/gpu-programming',
			demoHref: null,
			icon: Layers,
			tags: ['CUDA', 'C++', 'HPC'],
			categories: ['ongoing', 'build', 'gpu']
		},
		{
			title: 'Building Cool learning Platform',
			description: 'Building Cool learning Platform to learn by building real-world software',
			href: '#',
			demoHref: null,
			icon: Box,
			tags: ['Systems', 'Education', 'Go'],
			categories: ['build', 'ongoing', 'linux']
		},
		{
			title: 'Github Actions & Terraform',
			description: 'Infrastructure as code with automated deployment workflows',
			href: '#',
			demoHref: null,
			icon: Server,
			tags: ['IaC', 'CI/CD', 'Cloud'],
			categories: ['ongoing', 'devops']
		},
		{
			title: 'Building Pytorch',
			description: 'Understanding deep learning frameworks by implementing core components',
			href: '#',
			demoHref: null,
			icon: Cpu,
			tags: ['ML', 'Python', 'Autograd'],
			categories: ['ai', 'build', 'ongoing']
		},
		{
			title: 'Golang X Projects',
			description: 'Collection of projects exploring Go for systems programming',
			href: 'https://github.com/john221wick/golangXprojects',
			demoHref: null,
			icon: Code2,
			tags: ['Go', 'Systems', 'CLI'],
			categories: ['build', 'finished', 'linux']
		}
	];

	$: categoryCounts = categories.reduce((acc, category) => {
		if (category.id === 'all') {
			acc[category.id] = projectsOngoing.length;
			return acc;
		}
		acc[category.id] = projectsOngoing.filter((project) =>
			project.categories.includes(category.id)
		).length;
		return acc;
	}, {});

	$: filteredProjects =
		selectedCategory === 'all'
			? projectsOngoing
			: projectsOngoing.filter((project) => project.categories.includes(selectedCategory));
</script>

<div class="flex w-full flex-col gap-8 py-4 sm:py-8" in:fly={{ y: 20, duration: 500, delay: 100 }}>
	<!-- Header -->
	<section class="flex flex-col gap-4">
		<div class="flex items-center gap-2">
			<FolderGit2 class="h-5 w-5 text-zinc-500 dark:text-zinc-400" />
			<div class="min-w-0">
				<h1 class="text-lg font-semibold text-zinc-900 dark:text-white">Projects</h1>
				<p class="text-sm text-zinc-600 dark:text-zinc-400">Things I'm building and exploring</p>
			</div>
		</div>
	</section>

	<!-- Category Filter -->
	<section class="flex flex-col gap-3">
		<div class="flex items-center justify-between sm:hidden">
			<p class="text-xs font-medium text-zinc-600 dark:text-zinc-300">
				Filter: {categories.find((category) => category.id === selectedCategory)?.label}
			</p>
			<button
				type="button"
				class="inline-flex items-center gap-2 rounded-full border border-zinc-200 px-3 py-1.5 text-xs font-medium text-zinc-700 transition hover:border-zinc-300 hover:bg-zinc-50 dark:border-white/10 dark:text-zinc-200 dark:hover:border-white/20 dark:hover:bg-white/5"
				onclick={() => (showFilters = !showFilters)}
			>
				<span>{showFilters ? 'Hide filters' : 'Show filters'}</span>
			</button>
		</div>
		<div class={`${showFilters ? 'block' : 'hidden'} sm:block`}>
			<div class="flex flex-wrap gap-2">
				{#each categories as category}
					<button
						type="button"
						class={`inline-flex items-center gap-2 rounded-full border px-3 py-1.5 text-xs font-medium transition-all ${
							selectedCategory === category.id
								? 'border-zinc-900 bg-zinc-900 text-white dark:border-white dark:bg-white dark:text-zinc-900'
								: 'border-zinc-200 bg-white text-zinc-600 hover:border-zinc-300 hover:bg-zinc-50 dark:border-white/10 dark:bg-transparent dark:text-zinc-300 dark:hover:border-white/20 dark:hover:bg-white/5'
						}`}
						onclick={() => (selectedCategory = category.id)}
					>
						<span>{category.label}</span>
						<span
							class={`rounded-full px-2 py-0.5 text-[10px] ${
								selectedCategory === category.id
									? 'bg-white/15 text-white dark:bg-zinc-900/15 dark:text-zinc-900'
									: 'bg-zinc-100 text-zinc-600 dark:bg-white/10 dark:text-zinc-300'
							}`}
						>
							{categoryCounts[category.id]}
						</span>
					</button>
				{/each}
			</div>
			<p class="mt-2 text-xs text-zinc-500 dark:text-zinc-400">
				{categories.find((category) => category.id === selectedCategory)?.description}
			</p>
		</div>
	</section>

	<!-- Projects Grid -->
	<section class="stagger-children grid gap-4 sm:grid-cols-2">
		{#each filteredProjects as project}
			<article
				class="card-hover group flex flex-col gap-4 rounded-2xl border border-gray-200 bg-white p-5 dark:border-gray-800 dark:bg-gray-900"
			>
				<!-- Header -->
				<div class="flex items-start justify-between">
					<div class="rounded-xl bg-gray-100 p-2.5 dark:bg-gray-800">
						<project.icon class="h-5 w-5 text-gray-600 dark:text-gray-400" />
					</div>
					<div class="flex items-center gap-2">
						{#if project.href !== '#'}
							<a
								href={project.href}
								target="_blank"
								rel="noopener noreferrer"
								class="rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:hover:bg-gray-800 dark:hover:text-white"
								aria-label="View on GitHub"
							>
								<Github class="h-5 w-5" />
							</a>
						{/if}
						{#if project.demoHref && project.demoHref !== '#'}
							<a
								href={project.demoHref}
								target="_blank"
								rel="noopener noreferrer"
								class="rounded-lg p-2 text-gray-400 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:hover:bg-gray-800 dark:hover:text-white"
								aria-label="View demo"
							>
								<ExternalLink class="h-5 w-5" />
							</a>
						{/if}
					</div>
				</div>

				<!-- Content -->
				<div class="flex flex-col gap-2">
					<h2 class="font-semibold text-gray-900 dark:text-white">
						{project.title}
					</h2>
					<p class="line-clamp-2 text-sm leading-relaxed text-gray-600 dark:text-gray-400">
						{project.description}
					</p>
				</div>

				<!-- Tags -->
				<div class="mt-auto flex flex-wrap gap-2">
					{#each project.tags as tag}
						<span
							class="rounded-full bg-gray-100 px-2.5 py-1 text-xs font-medium text-gray-600 dark:bg-gray-800 dark:text-gray-400"
						>
							{tag}
						</span>
					{/each}
				</div>
			</article>
		{/each}
	</section>

	<!-- GitHub CTA -->
	<section
		class="flex flex-col items-center gap-4 rounded-2xl border border-gray-200 bg-gradient-to-br from-gray-50 to-white p-6 text-center sm:p-8 dark:border-gray-800 dark:from-gray-900 dark:to-gray-800"
	>
		<div class="rounded-full bg-gray-900 p-3 dark:bg-white">
			<Github class="h-6 w-6 text-white dark:text-gray-900" />
		</div>
		<div>
			<h3 class="text-lg font-semibold text-gray-900 dark:text-white">Want to see more?</h3>
			<p class="text-sm text-gray-600 dark:text-gray-400">
				Check out my GitHub for all projects and contributions
			</p>
		</div>
		<a
			href="https://github.com/john221wick"
			target="_blank"
			rel="noopener noreferrer"
			class="inline-flex items-center gap-2 rounded-xl bg-gray-900 px-5 py-2.5 text-sm font-medium text-white transition-all hover:bg-gray-800 dark:bg-white dark:text-gray-900 dark:hover:bg-gray-100"
		>
			<span>Visit GitHub</span>
			<ExternalLink class="h-4 w-4" />
		</a>
	</section>
</div>
