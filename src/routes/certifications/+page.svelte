<script>
	import { fly } from 'svelte/transition';
	import { marked } from 'marked';
	import Prism from 'prismjs';
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import 'prismjs/themes/prism-tomorrow.css';
	import 'prismjs/plugins/autoloader/prism-autoloader';
	import { Award, BookOpen, ExternalLink, Calendar, X, FileText } from 'lucide-svelte';

	onMount(() => {
		Prism.plugins.autoloader.languages_path =
			'https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/';
	});

	let posts = [
		{
			date: 'April 2025',
			title: 'GPU Architecture and Programming',
			institution: 'IIT Kharagpur',
			href: '/syllabi/gpu-programming.md',
			certHref: 'https://drive.google.com/file/d/1osecrPLUM18Xps4YD7U-SFsgPmr4Y5_M/view?usp=sharing'
		},
		{
			date: 'April 2025',
			title: 'Large Language Model',
			institution: 'IIT Kharagpur',
			href: '/syllabi/llm-syllabus.md',
			certHref: 'https://drive.google.com/file/d/1ooPebX8Gb6vn6yln84T0I5W0kho_5nmm/view?usp=sharing'
		},
		{
			date: 'April 2025',
			title: 'Image Processing with Python',
			institution: 'Online',
			href: '/syllabi/image-processing-python.md',
			certHref: 'https://drive.google.com/file/d/1pQ8vRAbWERdYcreQrF-LmWoDMji0cjbx/view?usp=sharing'
		},
		{
			date: 'April 2024',
			title: 'Applied Accelerated AI',
			institution: 'IIT Palakkad & NVIDIA',
			href: '/syllabi/applied-accelerated-ml.md',
			certHref: 'https://drive.google.com/file/d/1sNASrD4_2LE5u9BvUOe6iFoc1xcM33J5/view?usp=sharing'
		},
		{
			date: 'May 2024',
			title: 'Linear Algebra through Geometry',
			institution: 'IISc Bangalore',
			href: '/syllabi/linear-algebra-geometry.md',
			certHref: 'https://drive.google.com/file/d/1sQ1ao9MML9DGDTPgLIkNoN_8ZpAeX3e8/view?usp=sharing'
		},
		{
			date: 'April 2023',
			title: 'Blockchain and its Applications',
			institution: 'IIT Kharagpur',
			href: '/syllabi/blockchain.md',
			certHref: 'https://drive.google.com/file/d/17TjADjJWDIpLPIvcVod_I3EiohaN1bs2/view?usp=sharing'
		},
		{
			date: 'November 2022',
			title: 'Deep Learning',
			institution: 'IIT Ropar',
			href: '/syllabi/deep-learning.md',
			certHref: 'https://drive.google.com/file/d/1MQ6OE30keXZi5iFZ8qNmST9ob8cBcn23/view?usp=sharing'
		}
	];

	let postsCCompletion = [
		{
			date: 'August 2023',
			title: 'Serverless Computing with AWS Lambda',
			institution: 'AWS',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1pcBgDiBktK4wSO91YkX_oEG95uHkTtHK/view?usp=sharing'
		},
		{
			date: 'May 2023',
			title: 'Docker Training Course',
			institution: 'Docker',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1hX9188cnPLV5FhF3ORVrXjYvPgaK4lfc/view?usp=sharing'
		},
		{
			date: 'August 2023',
			title: 'Linux Administration',
			institution: 'Linux Foundation',
			href: '/post/svelte5/runes.md',
			certHref: 'https://drive.google.com/file/d/15gthFFfQG-7AtyK3CKKojysPLN19fSfI/view?usp=sharing'
		},
		{
			date: 'January 2024',
			title: 'CI/CD with GitHub Actions',
			institution: 'GitHub',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1htT-SGF-kki7OoOGM35c-v4QK4yc-DWI/view?usp=sharing'
		},
		{
			date: 'August 2023',
			title: 'Shell Programming (Bash)',
			institution: 'Linux',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1iqvRKZ-0Se7YdxJ3Ix4CQqRl53qY5_P3/view?usp=sharing'
		},
		{
			date: 'August 2023',
			title: 'Git and GitHub',
			institution: 'GitHub',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1N12gQIwJPEHUtVZhEdqbc1JI43r5u112/view?usp=sharing'
		},
		{
			date: 'June 2023',
			title: 'Pre Security Learning Path',
			institution: 'TryHackMe',
			href: '/test.md',
			certHref: 'https://drive.google.com/file/d/1BWmUjpT0vEYf6xWWVT8wdaNmOX5aEipU/view?usp=sharing'
		}
	];

	const sections = [
		{
			title: 'Certifications',
			subtitle: 'Recognised programs from universities and industry partners',
			icon: Award,
			accent: 'amber',
			items: posts
		},
		{
			title: 'Course Completions',
			subtitle: 'Self-paced learning and professional development',
			icon: BookOpen,
			accent: 'sky',
			items: postsCCompletion
		}
	];

	let markdownContent = $state(null);

	$effect(() => {
		const unsubscribe = page.subscribe((p) => {
			if (p.url.pathname === '/certifications') markdownContent = null;
		});
		return unsubscribe;
	});

	async function loadMarkdown(path) {
		try {
			const res = await fetch(path);
			if (!res.ok) throw new Error('Failed to fetch');
			const text = await res.text();
			markdownContent = marked.parse(text);
		} catch (err) {
			console.error(err);
			markdownContent = '<p class="text-red-500">Failed to load content.</p>';
		}
	}

	$effect(() => {
		if (!markdownContent) return;
		setTimeout(() => {
			document.querySelectorAll('pre code').forEach((block) => Prism.highlightElement(block));
		}, 0);
	});

	function closeMarkdown() {
		markdownContent = null;
	}

	// optional: keep stats auto
	const certCount = posts.length;
	const courseCount = postsCCompletion.length;
	const iitPrograms = [...posts, ...postsCCompletion].filter((x) =>
		/IIT/i.test(x.institution)
	).length;
</script>

{#if markdownContent}
	<!-- Minimal modal -->
	<div class="fixed inset-0 z-50 bg-black/50 p-2 backdrop-blur-sm sm:p-6" onclick={closeMarkdown}>
		<div
			class="mx-auto max-h-[92vh] w-full max-w-3xl overflow-hidden rounded-2xl bg-white ring-1 ring-zinc-200 dark:bg-zinc-950 dark:ring-white/10"
			onclick={(e) => e.stopPropagation()}
			in:fly={{ y: 10, duration: 180 }}
		>
			<div
				class="flex items-center justify-between border-b border-zinc-200 px-4 py-3 dark:border-white/10"
			>
				<p class="text-sm font-medium text-zinc-700 dark:text-zinc-200">Syllabus</p>
				<button
					class="rounded-lg p-2 text-zinc-500 hover:bg-zinc-100 dark:text-zinc-400 dark:hover:bg-white/10"
					onclick={closeMarkdown}
					aria-label="Close"
				>
					<X class="h-5 w-5" />
				</button>
			</div>

			<div class="max-h-[calc(92vh-52px)] overflow-y-auto px-3 py-4 sm:px-4 sm:py-5">
				<div
					class="prose prose-zinc dark:prose-invert prose-sm sm:prose-base prose-headings:mt-4 prose-headings:mb-2 prose-headings:leading-snug prose-ul:my-2 prose-li:my-1 max-w-none"
				>
					{@html markdownContent}
				</div>
			</div>
		</div>
	</div>
{/if}

<div
	class="mx-auto w-full max-w-4xl px-3 py-6 sm:py-10"
	in:fly={{ y: 12, duration: 300, delay: 50 }}
>
	<!-- <header class="mb-8">
		<h1 class="text-2xl font-semibold tracking-tight text-zinc-900 sm:text-3xl dark:text-white">
			Certifications & Learning
		</h1>
		<p class="mt-2 max-w-2xl text-sm leading-relaxed text-zinc-600 dark:text-zinc-400">
			Simple list — clean, readable, and mobile-friendly.
		</p>
	</header> -->

	<div class="flex flex-col gap-10">
		{#each sections as section}
			<section class="flex flex-col gap-4">
				<div class="flex items-center gap-2">
					<svelte:component this={section.icon} class="h-5 w-5 text-zinc-500 dark:text-zinc-400" />
					<div class="min-w-0">
						<h2 class="text-lg font-semibold text-zinc-900 dark:text-white">{section.title}</h2>
						<p class="text-sm text-zinc-600 dark:text-zinc-400">{section.subtitle}</p>
					</div>
				</div>

				<!-- Light list container -->
				<div
					class="overflow-hidden rounded-2xl border border-zinc-200 bg-white dark:border-white/10 dark:bg-zinc-950"
				>
					<div class="divide-y divide-zinc-200 dark:divide-white/10">
						{#each section.items as { date, title, institution, href, certHref }}
							<div class="p-4 sm:p-5">
								<div class="flex items-start justify-between gap-3">
									<!-- left: text -->
									<div class="min-w-0">
										<p class="truncate text-sm font-medium text-zinc-900 dark:text-white">
											{title}
										</p>
										<p
											class="mt-1 flex flex-wrap items-center gap-x-2 gap-y-1 text-xs text-zinc-600 dark:text-zinc-400"
										>
											<span class="truncate">{institution}</span>
											<span class="text-zinc-300 dark:text-zinc-700">•</span>
											<span class="inline-flex items-center gap-1">
												<Calendar class="h-3.5 w-3.5" />
												{date}
											</span>
										</p>
									</div>

									<!-- right: actions (mobile-safe) -->
									<div class="flex shrink-0 flex-col gap-2 sm:flex-row sm:items-center">
										<button
											type="button"
											class="inline-flex w-full items-center justify-center gap-2 rounded-xl border border-zinc-200 bg-transparent px-3 py-2 text-xs font-medium text-zinc-900 hover:bg-zinc-50 sm:w-auto dark:border-white/10 dark:text-zinc-200 dark:hover:bg-white/5"
											onclick={() => loadMarkdown(href)}
										>
											<FileText class="h-4 w-4" />
											<!-- <span>Notes</span> -->
										</button>

										<a
											href={certHref}
											target="_blank"
											rel="noopener noreferrer"
											aria-label="View certificate"
											class="inline-flex w-full items-center justify-center rounded-xl border border-zinc-200 bg-transparent px-3 py-2 text-zinc-900 hover:bg-zinc-50 sm:w-auto dark:border-white/10 dark:text-zinc-200 dark:hover:bg-white/5"
										>
											<ExternalLink class="h-4 w-4" />
										</a>
									</div>
								</div>
							</div>
						{/each}
					</div>
				</div>
			</section>
		{/each}

		<!-- Minimal stats -->
		<section
			class="rounded-2xl border border-zinc-200 bg-white p-4 sm:p-5 dark:border-white/10 dark:bg-zinc-950"
		>
			<div class="grid grid-cols-2 gap-4 sm:grid-cols-4">
				<div>
					<p class="text-lg font-semibold text-zinc-900 dark:text-white">{certCount}</p>
					<p class="text-xs text-zinc-600 dark:text-zinc-400">Certifications</p>
				</div>
				<div>
					<p class="text-lg font-semibold text-zinc-900 dark:text-white">{courseCount}</p>
					<p class="text-xs text-zinc-600 dark:text-zinc-400">Courses</p>
				</div>
				<div>
					<p class="text-lg font-semibold text-zinc-900 dark:text-white">{iitPrograms}+</p>
					<p class="text-xs text-zinc-600 dark:text-zinc-400">IIT programs</p>
				</div>
				<div>
					<p class="text-lg font-semibold text-zinc-900 dark:text-white">2022</p>
					<p class="text-xs text-zinc-600 dark:text-zinc-400">Since</p>
				</div>
			</div>
		</section>
	</div>
</div>
