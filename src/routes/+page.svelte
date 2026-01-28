<script>
	import { fly } from 'svelte/transition';
	import { ArrowRight, MapPin, GraduationCap } from 'lucide-svelte';
</script>

<div
	class="mx-auto w-full max-w-4xl px-3 py-6 sm:px-4 sm:py-10"
	in:fly={{ y: 12, duration: 320, delay: 60 }}
>
	<!-- Hero -->
	<section class="flex flex-col gap-6">
		<!-- Quiet status -->
		<div class="inline-flex items-center gap-2">
			<span class="h-2 w-2 rounded-full bg-emerald-500" />
			<span class="text-sm text-zinc-600 dark:text-zinc-400">Open to opportunities</span>
		</div>

		<div class="flex flex-col gap-3">
			<p class="text-sm text-zinc-600 dark:text-zinc-400">
				Hello <span class="wave-animation inline-block">👋</span>
			</p>

			<h1 class="text-4xl font-semibold tracking-tight text-zinc-900 sm:text-5xl dark:text-white">
				I’m <span class="underline decoration-zinc-300 underline-offset-8 dark:decoration-zinc-700"
					>Bhushan</span
				>
			</h1>

			<p class="max-w-2xl text-base leading-relaxed text-zinc-600 sm:text-lg dark:text-zinc-400">
				I build at the intersection of <span class="text-zinc-900 dark:text-white">AI</span>,
				<span class="text-zinc-900 dark:text-white">machine learning</span>, and
				<span class="text-zinc-900 dark:text-white">infrastructure</span>.
			</p>
		</div>

		<!-- Metadata row (instead of pills) -->
		<div
			class="flex flex-col gap-2 text-sm text-zinc-600 sm:flex-row sm:items-center sm:gap-5 dark:text-zinc-400"
		>
			<div class="inline-flex items-center gap-2">
				<GraduationCap class="h-4 w-4 text-zinc-500 dark:text-zinc-400" />
				<span>4th Year B.Tech Student</span>
			</div>
			<div class="hidden h-4 w-px bg-zinc-200 sm:block dark:bg-white/10" />
			<div class="inline-flex items-center gap-2">
				<MapPin class="h-4 w-4 text-zinc-500 dark:text-zinc-400" />
				<span>Central University of Haryana</span>
			</div>
		</div>
	</section>

	<!-- About -->
	<section class="mt-10">
		<h2 class="text-xs font-medium tracking-widest text-zinc-500 uppercase dark:text-zinc-500">
			About
		</h2>

		<div
			class="mt-3 border-l border-zinc-200 pl-4 text-zinc-700 dark:border-white/10 dark:text-zinc-300"
		>
			<p class="leading-relaxed">
				I’m currently working with <span class="font-medium text-zinc-900 dark:text-white"
					>MLOps</span
				>, building <span class="font-medium text-zinc-900 dark:text-white">AI agents</span> and
				<span class="font-medium text-zinc-900 dark:text-white">LLMs</span>, while exploring the
				<span class="font-medium text-zinc-900 dark:text-white">DevOps</span> ecosystem. I enjoy building
				projects from scratch to understand fundamentals and how systems behave under real constraints.
			</p>
		</div>
	</section>

	<!-- CTA -->
	<section class="mt-10 flex flex-col gap-3 sm:flex-row sm:items-center">
		<a
			href="/projects"
			class="inline-flex w-full items-center justify-center gap-2 rounded-xl bg-zinc-900 px-5 py-3 text-sm font-medium text-white hover:bg-zinc-800 sm:w-auto dark:bg-white dark:text-zinc-900 dark:hover:bg-zinc-200"
		>
			<span>View projects</span>
			<ArrowRight class="h-4 w-4" />
		</a>

		<a
			href="/certifications"
			class="inline-flex w-full items-center justify-center rounded-xl border border-zinc-200 px-5 py-3 text-sm font-medium text-zinc-800 hover:bg-zinc-50 sm:w-auto dark:border-white/10 dark:text-zinc-200 dark:hover:bg-white/5"
		>
			Certifications
		</a>
	</section>

	<p class="mt-8 text-xs text-zinc-500 dark:text-zinc-600">
		This portfolio is under active development.
	</p>
</div>

<style>
	.wave-animation {
		animation-name: wave-animation;
		animation-duration: 2.5s;
		animation-iteration-count: infinite;
		transform-origin: 70% 70%;
	}
	@keyframes wave-animation {
		0% {
			transform: rotate(0deg);
		}
		10% {
			transform: rotate(14deg);
		}
		20% {
			transform: rotate(-8deg);
		}
		30% {
			transform: rotate(14deg);
		}
		40% {
			transform: rotate(-4deg);
		}
		50% {
			transform: rotate(10deg);
		}
		60%,
		100% {
			transform: rotate(0deg);
		}
	}
</style>
