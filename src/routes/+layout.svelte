<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import { onMount } from 'svelte';
	import { page } from '$app/stores';

	let { children } = $props();

	let scrollY = $state(0);
	let scrollProgress = $state(0); // 0 = fully expanded, 1 = fully collapsed
	let isMobileMenuOpen = $state(false);
	let daysUntilWedding = $state(0);
	let showCountdown = $state(true);

	const navItems = [
		{ name: 'Home', href: '/' },
		{ name: 'Our Story', href: '/our-story' },
		{ name: 'Photos', href: '/photos' },
		{ name: 'Q + A', href: '/qa' },
		{ name: 'Travel', href: '/travel' },
		{ name: 'Things to Do', href: '/things-to-do' },
		{ name: 'Registry', href: '/registry' }
	];

	onMount(() => {
		const handleScroll = () => {
			scrollY = window.scrollY;
			// Gradual transition between 50px and 300px scroll
			const minScroll = 50;
			const maxScroll = 300;
			scrollProgress = Math.min(Math.max((scrollY - minScroll) / (maxScroll - minScroll), 0), 1);
		};

		const calculateDaysUntilWedding = () => {
			const weddingDate = new Date('2026-08-01');
			const today = new Date();
			const timeDifference = weddingDate.getTime() - today.getTime();
			const daysDifference = Math.ceil(timeDifference / (1000 * 3600 * 24));
			
			if (daysDifference <= 0) {
				showCountdown = false;
			} else {
				daysUntilWedding = daysDifference;
				showCountdown = true;
			}
		};

		// Calculate initial days
		calculateDaysUntilWedding();

		// Update daily at midnight
		const updateInterval = setInterval(calculateDaysUntilWedding, 24 * 60 * 60 * 1000);

		window.addEventListener('scroll', handleScroll);
		
		return () => {
			window.removeEventListener('scroll', handleScroll);
			clearInterval(updateInterval);
		};
	});

	function toggleMobileMenu() {
		isMobileMenuOpen = !isMobileMenuOpen;
	}

	function closeMobileMenu() {
		isMobileMenuOpen = false;
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;500;600;700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="min-h-screen m-6 bg-white">
	<!-- Desktop Navigation -->
	<nav
		class="fixed top-0 right-0 left-0 z-50 transition-all duration-500 ease-out hidden md:block"
		style="
			background-color: rgba(255, 255, 255, {(scrollProgress / scrollProgress) * 0.95});
			backdrop-filter: blur({scrollProgress * 4}px);
			box-shadow: 0 1px 3px rgba(0, 0, 0, {scrollProgress * 0.1});
			padding-top: {6 - scrollProgress * 6}rem;
			padding-bottom: {6 - scrollProgress * 6}rem;
		"
	>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<!-- Single unified layout that transforms -->
			<div class="relative">
				<!-- Names - Always on top and centered, slide left as user scrolls -->
				<div class="mb-4 text-center">
					<h1
						class="tracking-wider text-black transition-all duration-500 ease-out"
						style="
							font-family: 'Dancing Script', cursive; 
							font-weight: 600;
							font-size: {4.5 - scrollProgress * 1.5}rem;
							transform: translate({scrollProgress * -40}%, {scrollProgress * 30}%);
						"
					>
						<a href="/" class="transition-colors duration-200 hover:text-gray-600">
							Gabriel & Elyse
						</a>
					</h1>
				</div>

				<!-- Wedding Information - Folds up as user scrolls -->
				<div
					class="overflow-hidden text-center transition-all duration-500 ease-out"
					style="
						max-height: {(1 - scrollProgress) * 200}px;
						opacity: {1 - scrollProgress * 1.5};
						transform: translateY({scrollProgress * -30}px) scaleY({1 - scrollProgress * 0.3});
						margin-bottom: {(1 - scrollProgress) * 2}rem;
					"
				>
					<p
						class="mb-2 text-lg font-light text-gray-600 transition-all duration-500 ease-out sm:text-xl"
						style="
							transform: translateY({scrollProgress * -20}px);
						"
					>
						August 1, 2026 • Cashiers, NC, USA
					</p>
					{#if showCountdown}
						<p
							class="text-base text-gray-500 transition-all duration-500 ease-out"
							style="
								transform: translateY({scrollProgress * -15}px);
							"
						>
							{daysUntilWedding} Day{daysUntilWedding === 1 ? '' : 's'} To Go!
						</p>
					{/if}
				</div>

				<!-- Navigation Links - Slide from center to right -->
				<div>
					<div
						class="flex justify-center space-x-8 transition-all duration-500 ease-out"
						style="
							transform: translate({scrollProgress * 30}%, {scrollProgress * -175}%);
						"

					>
						{#each navItems as item}
							<a
								href={item.href}
								class="font-light tracking-wide text-black transition-colors duration-200 hover:text-gray-600 {$page
									.url.pathname === item.href
									? 'border-b border-black'
									: ''}"
							>
								{item.name}
							</a>
						{/each}
					</div>
				</div>
			</div>
		</div>
	</nav>

	<!-- Mobile Navigation -->
	<nav class="fixed top-0 left-0 right-0 z-50 md:hidden bg-white/95 backdrop-blur-sm shadow-sm">
		<div class="mx-auto max-w-7xl px-4 py-3">
			<div class="flex items-center justify-between">
				<!-- Names -->
				<div class="flex-shrink-0">
					<h1 class="text-lg tracking-wider text-black" style="font-family: 'Dancing Script', cursive; font-weight: 600;">
						<a href="/" class="transition-colors duration-200 hover:text-gray-600">
							Gabriel & Elyse
						</a>
					</h1>
				</div>

				<!-- Wedding Info -->
				<div class="flex-1 text-center px-4">
					<p class="text-xs text-gray-600 font-light">Aug 1, 2026 • NC</p>
					{#if showCountdown}
						<p class="text-xs text-gray-500">{daysUntilWedding} days to go!</p>
					{/if}
				</div>

				<!-- Menu Button -->
				<div class="flex-shrink-0">
					<button
						onclick={toggleMobileMenu}
						class="text-black transition-colors duration-200 hover:text-gray-600 p-2"
						aria-label="Toggle menu"
					>
						<svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							{#if isMobileMenuOpen}
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M6 18L18 6M6 6l12 12"
								/>
							{:else}
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M4 6h16M4 12h16M4 18h16"
								/>
							{/if}
						</svg>
					</button>
				</div>
			</div>
		</div>

		<!-- Mobile Navigation Menu -->
		<div
			class="overflow-hidden transition-all duration-300 ease-in-out {isMobileMenuOpen
				? 'max-h-96 opacity-100'
				: 'max-h-0 opacity-0'}"
		>
			<div
				class="transform border-t border-gray-100 bg-white/95 backdrop-blur-sm transition-transform duration-300 ease-in-out {isMobileMenuOpen
					? 'translate-y-0'
					: '-translate-y-4'}"
			>
				<div class="px-4 py-4">
					{#each navItems as item}
						<a
							href={item.href}
							onclick={closeMobileMenu}
							class="block transform py-3 font-light tracking-wide text-black transition-all duration-200 hover:text-gray-600 {isMobileMenuOpen
								? 'translate-x-0 opacity-100'
								: 'translate-x-4 opacity-0'} {$page.url.pathname === item.href
								? 'border-l-2 border-black pl-4'
								: 'pl-2'}"
						>
							{item.name}
						</a>
					{/each}
				</div>
			</div>
		</div>
	</nav>

	<!-- Main Content -->
	<main class="pt-20 md:pt-0">
		<div class="hidden md:block transition-all duration-500 ease-out" style="padding-top: {20 - scrollProgress * 12}rem;"></div>
		{@render children?.()}
	</main>

	<!-- Footer -->
	<footer class="border-t border-gray-100 bg-gray-50">
		<div class="mx-auto max-w-7xl px-4 py-12 sm:px-6 lg:px-8">
			<div class="text-center">
				<h3
					class="mb-2 text-2xl text-black"
					style="font-family: 'Dancing Script', cursive; font-weight: 600;"
				>
					Gabriel & Elyse Timotei
				</h3>
				<p class="mb-4 text-gray-600">August 1, 2026 • Cashiers, NC, USA</p>
				<p class="text-sm text-gray-500">We can't wait to celebrate with you!</p>
			</div>
		</div>
	</footer>
</div>
