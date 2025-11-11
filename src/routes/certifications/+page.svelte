<script>
	import { marked } from 'marked';
	import Prism from 'prismjs';
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import 'prismjs/themes/prism-tomorrow.css';
	import 'prismjs/plugins/autoloader/prism-autoloader';

	onMount(() => {
		Prism.plugins.autoloader.languages_path =
			'https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/';
	});

	let posts = [
		{
			date: 'April 28, 2025',
			title: 'GPU Architecture and Programming (IIT Kharagpur)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1osecrPLUM18Xps4YD7U-SFsgPmr4Y5_M/view?usp=sharing'
		},
		{
			date: 'April 28, 2025',
			title: 'Large Language Model (IIT Kharagpur)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1ooPebX8Gb6vn6yln84T0I5W0kho_5nmm/view?usp=sharing'
		},
		{
			date: 'April 28, 2025',
			title: 'Image Processing with python',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1pQ8vRAbWERdYcreQrF-LmWoDMji0cjbx/view?usp=sharing'
		},
		{
			date: 'April 9, 2024',
			title: 'Applied Accelerated Artificial Intelligence (IIT Palakkad) (NVIDIA)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1sNASrD4_2LE5u9BvUOe6iFoc1xcM33J5/view?usp=sharing'
		},
		{
			date: 'May 15, 2024',
			title: 'Linear algebra through Geometry (IISc Banglore) (one of the best course)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1sQ1ao9MML9DGDTPgLIkNoN_8ZpAeX3e8/view?usp=sharing'
		},
		{
			date: 'April, 2023',
			title: 'BlockChain and its application (IIT Kharagpur)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/17TjADjJWDIpLPIvcVod_I3EiohaN1bs2/view?usp=sharing'
		},
		{
			date: 'November, 2022',
			title: 'Deep Learning (IIT Ropar)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1MQ6OE30keXZi5iFZ8qNmST9ob8cBcn23/view?usp=sharing'
		}
	];

	let postsCCompletion = [
		{
			date: 'Aug 8, 2023',
			title: 'Serverless Computing with AWS Lambda',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1pcBgDiBktK4wSO91YkX_oEG95uHkTtHK/view?usp=sharing'
		},
		{
			date: 'May 29, 2023',
			title: 'Docker Training Course',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1hX9188cnPLV5FhF3ORVrXjYvPgaK4lfc/view?usp=sharing'
		},
		{
			date: 'August 22, 2023',
			title: 'Linux Course',
			href: '/post/svelte5/runes.md',
			certHref: 'https://drive.google.com/file/d/15gthFFfQG-7AtyK3CKKojysPLN19fSfI/view?usp=sharing'
		},
		{
			date: 'January, 2024',
			title: 'CI/CD with Github actions',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1htT-SGF-kki7OoOGM35c-v4QK4yc-DWI/view?usp=sharing'
		},
		{
			date: 'August 28, 2023',
			title: 'Shell Programming (Bash)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1iqvRKZ-0Se7YdxJ3Ix4CQqRl53qY5_P3/view?usp=sharing'
		},
		{
			date: 'August 28, 2023',
			title: 'Git and Github',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1N12gQIwJPEHUtVZhEdqbc1JI43r5u112/view?usp=sharing'
		},
		{
			date: 'June 27, 2023',
			title: 'Try Hack Me (Pre Security Learning Path)',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1BWmUjpT0vEYf6xWWVT8wdaNmOX5aEipU/view?usp=sharing'
		}
	];

	let markdownContent = $state(null);

	$effect(() => {
		const unsubscribe = page.subscribe((p) => {
			if (p.url.pathname === '/certifications') {
				markdownContent = null;
			}
		});
		return unsubscribe;
	});

	async function loadMarkdown(path) {
		try {
			const res = await fetch(path);
			if (!res.ok) {
				throw new Error('Failed to fetch');
			}
			const text = await res.text();
			markdownContent = marked.parse(text);
		} catch (err) {
			console.error('Error loading Markdown:', err);
			markdownContent = '<p class="text-red-500">Failed to load content.</p>';
		}
	}

	$effect(() => {
		if (markdownContent) {
			setTimeout(() => {
				const codeBlocks = document.querySelectorAll('pre code');
				codeBlocks.forEach((block) => {
					Prism.highlightElement(block);
				});
			}, 0);
		}
	});

	const certificateIconPath =
		'M9 4.5a.75.75 0 0 1 .75.75v1.51a3 3 0 0 1 4.5 0V5.25a.75.75 0 0 1 1.5 0v1.51a3 3 0 0 1 4.5 0V5.25a.75.75 0 0 1 1.5 0v1.62c.394.204.774.43.1.666l.006.007c.833.475 1.494 1.252 1.91 2.162.415.91.415 1.92 0 2.83-.416.91-1.077 1.687-1.91 2.162l-.006.007a11.95 11.95 0 0 1-1.11-.666v1.62a.75.75 0 0 1-1.5 0v-1.51a3.001 3.001 0 0 1-4.5 0v1.51a.75.75 0 0 1-1.5 0v-1.51a3 3 0 0 1-4.5 0v1.51a.75.75 0 0 1-1.5 0v-1.62a11.95 11.95 0 0 1-1.11-.666l-.006-.007c-.833-.475-1.494-1.252-1.91-2.162a2.98 2.98 0 0 1 0-2.83c.416-.91 1.077-1.687 1.91-2.162l.006-.007c.336-.192.716-.422 1.11-.666V4.5a.75.75 0 0 1 .75-.75Zm1.5 3.99a1.5 1.5 0 0 0-3 0V15a1.5 1.5 0 0 0 3 0V8.49Zm4.5 0a1.5 1.5 0 0 0-3 0V15a1.5 1.5 0 0 0 3 0V8.49Z';

	const documentIconPath =
		'M3.75 3A1.75 1.75 0 0 0 2 4.75v14.5A1.75 1.75 0 0 0 3.75 21h12.5A1.75 1.75 0 0 0 18 19.25V7.5L13 3H3.75zM3.5 4.75a.25.25 0 0 1 .25-.25h8.5a.75.75 0 0 1 .75.75v3.5a.75.75 0 0 1-.75.75h-3.25a.75.75 0 0 1-.75-.75V4.75zm5.75.5h2.5v2.5h-2.5V5.25z';
</script>

{#if markdownContent}
	<div
		class="prose dark:prose-invert prose-gray mx-auto max-w-2xl rounded-lg
				bg-white p-4
				text-gray-800 shadow-md sm:p-8
				dark:bg-neutral-900 dark:text-gray-200"
	>
		{@html markdownContent}
	</div>
{:else}
	<section class="mx-auto w-full max-w-3xl px-4 py-2">
		<!-- Certifications -->
		<div>
			<h2
				class="mb-8 text-xl text-gray-900 sm:text-2xl
				md:text-3xl dark:text-white"
			>
				Certifications
			</h2>

			<div class="flex flex-col space-y-6">
				{#each posts as { date, title, href, certHref } (title)}
					<div
						class="flex w-full flex-col items-start
						justify-between gap-y-3 sm:flex-row sm:items-center"
					>
						<!-- Title -->
						<a
							{href}
							onclick={(e) => {
								e.preventDefault();
								loadMarkdown(href);
							}}
							class="group flex cursor-pointer items-center gap-x-3 text-left"
						>
							<svg
								class="h-5 w-5 text-gray-500 dark:text-neutral-400"
								fill="currentColor"
								viewBox="0 0 20 20"
							>
								<path d={documentIconPath}></path>
							</svg>

							<h2 class="text-gray-900 group-hover:underline dark:text-neutral-100">
								{title}
							</h2>
						</a>

						<!-- Right Section -->
						<div
							class="flex w-full items-center justify-between gap-x-6
							pl-8 sm:w-auto sm:justify-end sm:pl-0"
						>
							<span class="min-w-fit text-sm text-gray-500 dark:text-neutral-400">
								{date}
							</span>

							{#if certHref !== 'a'}
								<a
									href={certHref}
									target="_blank"
									rel="noopener noreferrer"
									class="group flex items-center gap-x-1.5 rounded-full border
									border-gray-300 bg-gray-100
									px-3 py-1
									text-sm text-gray-700 transition-colors
									hover:border-gray-500 hover:bg-gray-200
									hover:text-black
									dark:border-neutral-700 dark:bg-neutral-800/50
									dark:text-neutral-300 dark:hover:border-neutral-500
									dark:hover:bg-neutral-800 dark:hover:text-white"
								>
									<svg class="h-4 w-4" fill="currentColor" viewBox="0 0 24 24">
										<path d={certificateIconPath}></path>
									</svg>
									<span>View</span>
								</a>
							{/if}
						</div>
					</div>
				{/each}
			</div>
		</div>

		<!-- Course Completion -->
		<div class="mt-12">
			<h2
				class="mb-8 text-xl text-gray-900 sm:text-2xl
				md:text-3xl dark:text-white"
			>
				Course Completion
			</h2>

			<div class="flex flex-col space-y-6">
				{#each postsCCompletion as { date, title, href, certHref } (title)}
					<div
						class="flex w-full flex-col items-start
						justify-between gap-y-3 sm:flex-row sm:items-center"
					>
						<a
							{href}
							onclick={(e) => {
								e.preventDefault();
								loadMarkdown(href);
							}}
							class="group flex cursor-pointer items-center gap-x-3 text-left"
						>
							<svg
								class="h-5 w-5 text-gray-500 dark:text-neutral-400"
								fill="currentColor"
								viewBox="0 0 20 20"
							>
								<path d={documentIconPath}></path>
							</svg>

							<h2 class="text-gray-900 group-hover:underline dark:text-neutral-100">
								{title}
							</h2>
						</a>

						<div
							class="flex w-full items-center justify-between gap-x-6
							pl-8 sm:w-auto sm:justify-end sm:pl-0"
						>
							<span class="min-w-fit text-sm text-gray-500 dark:text-neutral-400">
								{date}
							</span>

							{#if certHref}
								<a
									href={certHref}
									target="_blank"
									rel="noopener noreferrer"
									class="group flex items-center gap-x-1.5 rounded-full border
									border-gray-300 bg-gray-100
									px-3 py-1
									text-sm text-gray-700 transition-colors
									hover:border-gray-500 hover:bg-gray-200
									hover:text-black
									dark:border-neutral-700 dark:bg-neutral-800/50
									dark:text-neutral-300 dark:hover:border-neutral-500
									dark:hover:bg-neutral-800 dark:hover:text-white"
								>
									<svg class="h-4 w-4" fill="currentColor" viewBox="0 0 24 24">
										<path d={certificateIconPath}></path>
									</svg>
									<span>View</span>
								</a>
							{/if}
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>
{/if}
