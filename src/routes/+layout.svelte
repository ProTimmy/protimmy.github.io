<script lang="ts">
	import '../app.css';
	const favicon = '/favicon.svg';
	import { onMount } from 'svelte';
	import { page } from '$app/stores';

	let { children } = $props();

	let scrollProgress = $state(false); // 0 = fully expanded, 1 = fully collapsed
	let isMobileMenuOpen = $state(false);
	let daysUntilWedding = $state(0);
	let showCountdown = $state(true);
	const iframeRoutes = ['/rsvp'];
	const isIframeRoute = $derived(iframeRoutes.includes($page.url.pathname));
	const isDesktopViewport = $derived.by(() => {
		if (typeof window === 'undefined') return true;
		return window.matchMedia('(min-width: 1024px)').matches;
	});
	const isNavCollapsed = $derived(scrollProgress && !isIframeRoute);
	let iframeTopOffset = $state(0);
	let desktopNavEl: HTMLElement | null = null;
	let mobileNavEl: HTMLElement | null = null;

	function updateIframeOffset() {
		if (typeof window === 'undefined') return;
		const isDesktop = window.matchMedia('(min-width: 1024px)').matches;
		const activeNav = isDesktop ? desktopNavEl : mobileNavEl;
		if (!activeNav) return;
		// Mobile nav is sticky and remains in normal flow, so no extra top offset is needed.
		iframeTopOffset = isDesktop ? Math.max(0, Math.ceil(activeNav.getBoundingClientRect().bottom)) : 0;
	}

	const navItems = [
		{ name: 'Home', href: '/' },
		{ name: 'RSVP', href: '/rsvp' },
		{ name: 'Our Story', href: '/our-story' },
		{ name: 'Q + A', href: '/qa' },
		{ name: 'Travel', href: '/travel' },
		{ name: 'Things to Do', href: '/things-to-do' },
		{ name: 'Registry', href: 'https://withjoy.com/gabriel-and-elyse/registry' },
		{ name: 'Wedding Photos', href: '/photos' },
	];

	onMount(() => {
		const maxScroll = 20;
		scrollProgress = document.body.scrollTop >= maxScroll || document.documentElement.scrollTop >= maxScroll ? true : false;

		const handleScroll = () => {
			scrollProgress = document.body.scrollTop >= maxScroll || document.documentElement.scrollTop >= maxScroll ? true : false;
			updateIframeOffset();
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
		updateIframeOffset();

		// Update daily at midnight
		const updateInterval = setInterval(calculateDaysUntilWedding, 24 * 60 * 60 * 1000);

		window.addEventListener('scroll', handleScroll);
		window.addEventListener('resize', updateIframeOffset);
		
		return () => {
			window.removeEventListener('scroll', handleScroll);
			window.removeEventListener('resize', updateIframeOffset);
			clearInterval(updateInterval);
		};
	});

	$effect(() => {
		if (!isIframeRoute || typeof window === 'undefined') return;
		window.scrollTo(0, 0);
		// Run after DOM/nav transitions settle so iframe top padding is accurate on route re-entry.
		const raf1 = requestAnimationFrame(() => {
			updateIframeOffset();
			requestAnimationFrame(updateIframeOffset);
		});
		return () => cancelAnimationFrame(raf1);
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

<div class="p-6 bg-black">
	<div class="bg-white">
		<!-- Desktop Navigation -->
		<nav
			bind:this={desktopNavEl}
			class="fixed transition-all duration-500 ease-out py-4 top-{isNavCollapsed ? 0 : 6} left-6 right-6 z-50 hidden lg:block"
			style="
				background-color: rgba(255, 255, 255, 0.95);
				backdrop-filter: blur(4px);
				box-shadow: 0 1px 3px rgba(0, 0, 0, {isNavCollapsed ? 0.1 : 0});
			"
		>
			<div class="mx-auto max-w-7xl transition-all duration-500 ease-out pr-45 pl-30 xl:pl-45">
				<!-- Single unified layout that transforms -->
				<div class="relative">
					<!-- Names - Always on top and centered, slide left as user scrolls -->
					<div class="mb-4 py-2 text-center">
						<h1
							class="tracking-wider text-black transition-all duration-500 ease-out"
							style="
								font-family: 'Dancing Script', cursive; 
								font-weight: 600;
								transform: translate({isNavCollapsed ? -40 : 0}%, {isNavCollapsed ? 30 : 0}%);
							"
						>
							<a href="/" class="transition-colors duration-200 hover:text-gray-600 {isNavCollapsed ? 'text-5xl' : 'text-6xl' }">
								Gabriel & Elyse
							</a>
						</h1>
					</div>

					<!-- Wedding Information - Folds up as user scrolls -->
					<div
						class="overflow-hidden text-center transition-all duration-500 ease-out"
						style="
							max-height: {isNavCollapsed ? 0 : 200}px;
							opacity: {isNavCollapsed ? 0 : 1};
							transform: translateY({isNavCollapsed ? -30 : 0}px) scaleY({isNavCollapsed ? 0.7 : 1});
						"
					>
						<p
							class="mb-2 text-lg font-light text-gray-600 transition-all duration-500 ease-out"
							style="
								transform: translateY({isNavCollapsed ? -20 : 0}px);
							"
						>
							August 1, 2026 • Glenville, NC, USA
						</p>
						{#if showCountdown}
							<p
								class="text-base mb-6 text-gray-500 transition-all duration-500 ease-out"
								style="
									transform: translateY({isNavCollapsed ? -15 : 0}px);
								"
							>
								{daysUntilWedding} Day{daysUntilWedding === 1 ? '' : 's'} To Go!
							</p>
						{/if}
					</div>

					<!-- Navigation Links - Slide from center to right -->
					<div
						class="flex justify-center space-x-8 transition-all duration-500 ease-out"
						style="
							transform: translate({isNavCollapsed ? 30 : 0}%, {isNavCollapsed ? -175 : 0}%);
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
		</nav>

		<!-- Mobile Navigation -->
		<nav bind:this={mobileNavEl} class="sticky top-0 left-0 right-0 z-50 lg:hidden bg-white/95 backdrop-blur-sm shadow-sm">
			<div class="mx-auto max-w-7xl px-4 py-3">
				<div class="flex items-center justify-between">
					<!-- Names -->
					<div class="flex-shrink-0">
						<h1 class="text-3xl tracking-wider text-black" style="font-family: 'Dancing Script', cursive; font-weight: 600;">
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
					? 'max-h-[min(85vh,32rem)] opacity-100'
					: 'max-h-0 opacity-0'}"
			>
				<div
					class="transform border-t border-gray-100 backdrop-blur-sm transition-transform duration-300 ease-in-out {isMobileMenuOpen
						? 'translate-y-0'
						: '-translate-y-4'}"
					style="background-color: rgba(255,255,255,0.95);"
				>
					<div class="px-4 pt-4 pb-8">
						{#each navItems as item}
							<a
								href={item.href}
								onclick={closeMobileMenu}
								class="block transform py-3.5 font-light tracking-wide text-black transition-all duration-200 hover:text-gray-600 {isMobileMenuOpen
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
		<main
			class="transition-all duration-500 ease-out box-border {isIframeRoute ? 'pt-0 overflow-hidden' : 'lg:pt-80 pt-10'}"
			style={isIframeRoute
				? `height: calc(100dvh - ${isDesktopViewport ? '3rem' : '0rem'}); padding-top: ${iframeTopOffset}px;`
				: ''}
		>
			{@render children?.()}
		</main>

		<!-- Footer -->
		{#if !isIframeRoute}
			<footer class="border-t border-gray-100 bg-gray-50">
				<div class="mx-auto max-w-7xl px-4 py-12 sm:px-6 lg:px-8">
					<div class="text-center">
						<h3
							class="mb-2 text-2xl text-black"
							style="font-family: 'Dancing Script', cursive; font-weight: 600;"
						>
							Gabriel & Elyse Timotei
						</h3>
						<p class="mb-4 text-gray-600">August 1, 2026 • Glenville, NC, USA</p>
						<p class="text-sm text-gray-500">We can't wait to celebrate with you!</p>
					</div>
				</div>
			</footer>
		{/if}
	</div>
</div>
