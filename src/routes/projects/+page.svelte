<script>
	let projectsOngoing = [
		{
			title: 'Agentic CI/CD',
			href: 'https://github.com/john221wick/agentic-ci-cd',
			demoHref: null
		},
		{
			title: 'Making miniGPT',
			href: 'https://github.com/john221wick/building-llm',
			demoHref: 'https://building-llm.vercel.app/'
		},
		{
			title: 'Leetcode clone',
			href: 'https://github.com/john221wick/cp-platform',
			demoHref: 'https://cp-platform-one.vercel.app/'
		},
		{
			title: 'GPU Programming',
			href: 'https://github.com/john221wick/gpu-programming',
			demoHref: null
		},
		{
			title: 'Building CodeCrafters Clone',
			href: '#',
			demoHref: '#'
		},
		{
			title: 'Github actions and Terraform',
			href: '#',
			demoHref: null
		},
		{
			title: 'Building Pytorch',
			href: '#',
			demoHref: '#'
		},
		{
			title: 'Building X Golang Projects',
			href: 'https://github.com/john221wick/golangXprojects',
			demoHref: null
		}
	];

	// SVG paths for the icons
	const githubIconPath =
		'M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z';

	const externalLinkIconPath =
		'M10.75 8.75a.75.75 0 0 0 0 1.5h1.5v1.5a.75.75 0 0 0 1.5 0v-1.5h1.5a.75.75 0 0 0 0-1.5h-1.5v-1.5a.75.75 0 0 0-1.5 0v1.5h-1.5z M4.5 2A2.5 2.5 0 0 0 2 4.5v9A2.5 2.5 0 0 0 4.5 16h9a2.5 2.5 0 0 0 2.5-2.5V9a.75.75 0 0 0-1.5 0v4.5a1 1 0 0 1-1 1h-9a1 1 0 0 1-1-1v-9a1 1 0 0 1 1-1h4.5a.75.75 0 0 0 0-1.5H4.5z';
</script>

<section class="w-full max-w-3xl px-2 py-2">
	<h1 class="mb-8 text-2xl font-medium text-gray-900 dark:text-white">Projects</h1>

	<div class="flex flex-col space-y-6">
		{#each projectsOngoing as project (project.title)}
			<div
				class="flex w-full flex-col items-start justify-between gap-y-3 sm:flex-row sm:items-center"
			>
				<a
					href={project.href}
					target="_blank"
					rel="noopener noreferrer"
					class="group flex items-center gap-x-3 transition-opacity hover:opacity-80"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						class="h-5 w-5 text-gray-500 dark:text-neutral-400"
						viewBox="0 0 16 16"
						fill="currentColor"
					>
						<path d={githubIconPath} />
					</svg>

					<h2 class="font-medium text-gray-900 group-hover:underline dark:text-neutral-100">
						{project.title}
					</h2>
				</a>

				{#if project.demoHref}
					<a
						href={project.demoHref}
						target="_blank"
						rel="noopener noreferrer"
						class="group flex items-center gap-x-2 rounded-full border
						border-gray-300 bg-gray-100
						px-3 py-1
						text-sm text-gray-700 transition-colors
						hover:border-gray-500 hover:bg-gray-200
						hover:text-black
						dark:border-neutral-700 dark:bg-neutral-800/50
						dark:text-neutral-300 dark:hover:border-neutral-500
						dark:hover:bg-neutral-800 dark:hover:text-white"
					>
						<span>View Demo</span>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							class="h-4 w-4 transition-transform group-hover:translate-x-0.5"
							viewBox="0 0 20 20"
							fill="currentColor"
						>
							<path d={externalLinkIconPath} />
						</svg>
					</a>
				{/if}
			</div>
		{/each}
	</div>
</section>
