<script lang="ts">
	const college_years_1 = '/our-story/college-years-1.JPG';
	const officially_official_1 = '/our-story/officially-official-1.jpg';
	const officially_official_2 = '/our-story/officially-official-2.jpeg';
	const officially_official_3 = '/our-story/officially-official-3.jpeg';
	const pandemic_1 = '/our-story/pandemic-1.JPG';
	const pandemic_2 = '/our-story/pandemic-2.jpeg';
	const pandemic_3 = '/our-story/pandemic-3.JPG';
	const pandemic_4 = '/our-story/pandemic-4.jpeg';
	const dc_1 = '/our-story/dc-1.jpeg';
	const dc_2 = '/our-story/dc-2.jpg';
	const dc_3 = '/our-story/dc-3.jpeg';
	const boston_1 = '/our-story/boston-1.jpeg';
	const boston_2 = '/our-story/boston-2.jpeg';
	const boston_3 = '/our-story/boston-3.JPG';
	const nyc_1 = '/our-story/nyc-1.jpeg';
	const nyc_2 = '/our-story/nyc-2.jpeg';
	const nyc_3 = '/our-story/nyc-3.jpeg';
	const nyc_4 = '/our-story/nyc-4.jpeg';
	const proposal_1 = '/our-story/proposal-1.JPG';
	const proposal_2 = '/our-story/proposal-2.jpeg';
	const proposal_3 = '/our-story/proposal-3.jpeg';

	interface TimelineEvent {
		date: string;
		title: string;
		description: string;
		photos?: {
			caption?: string;
			image: string;
		}[];
	}

	const timelineEvents: TimelineEvent[] = [
		{
			date: "Fall 2018",
			title: "And they were roommates...",
			description: "A bit unconventional, but we first met when we became roommates in college at UNC Chapel Hill. We instantly hit it off as friends, but it would take a while longer for love to blossom.",
			photos: [
				{
					caption: "First photo together",
					image: college_years_1
				},
			]
		},
		{
			date: "Summer 2019",
			title: "Officially official",
			description: "It wasn't until after Gabe had graduated that we began dating. We spent most of the summer apart while Gabe was on a road trip and started our new long distance relationship with lots of travel between DC and Chapel Hill.",
			photos: [
				{
					caption: "Date at Dorothea Dix park",
					image: officially_official_1
				},
				{
					image: officially_official_2
				},
				{
					caption: "Hiking trip in the Rocky Mountains",
					image: officially_official_3
				},
			]
		},
		{
			date: "March 2020",
			title: "And then there was a pandemic...",
			description: "The pandemic hit while we were on Elyse's spring break trip with friends in Colorado. Queue Gabe's crash course in Hickory, NC as we waited out the pandemic while Elyse graduated from her undergrad. We made the most of it, making it our goal to see as many National Parks as we could possibly visit!",
			photos: [
				{
					caption: "Elyse's remote graudation",
					image: pandemic_1
				},
				{
					caption: "Pandemic-style hiking",
					image: pandemic_2
				},
				{
					caption: "Our alien-themed van!",
					image: pandemic_3
				},
				{
					caption: "Glacier National Park, MT",
					image: pandemic_4
				},
			]
		},
		{
			date: "August 2020",
			title: "New family member!",
			description: "We kicked off a year of new adventures in DC with the addition of our kitty, Yoshi (named after Gabe's favorite Super Smash Bros character)! She brought a spark of joy and energy to an otherwise weird year as we waited out the rest of the pandemic.",
			photos: [
				{
					caption: "Meet Yoshi!",
					image: dc_1
				},
				{
					caption: "Taking Yoshi for a ride",
					image: dc_2
				},
				{
					caption: "Anniversary dinner at Fiola, DC",
					image: dc_3
				},
			]
		},
		{
			date: "August 2021",
			title: "HAVAHD",
			description: "Elyse decided to enroll in a small school in Cambridge, MA for her master's degree. We lived on-campus together for 2 years and experienced the best of what New England had to offer. We also made some great friends along the way, whose footsteps we would follow for our next move...",
			photos: [
				{
					caption: "Baseball at Fenway Park",
					image: boston_1
				},
				{
					caption: "Trip to Mexico with our friends",
					image: boston_2
				},
				{
					caption: "Elyse's Harvard graduation",
					image: boston_3
				},
			]
		},
		{
			date: "August 2023",
			title: "I'M WALKING HERE",
			description: "When most of our friends deserted Boston, we decided to follow them to NYC! We've made the most of our time in The Big Apple - going to Broadway shows, eating great food, and hosting weekly Survivor watch parties. We've really felt at home here thanks to our wonderful community and all that the city has to offer!",
			photos: [
				{
					caption: "Kebab party in our patio",
					image: nyc_1
				},
				{
					caption: "Views from Central Park",
					image: nyc_2
				},
				{
					caption: "Elyse's masquerade birthday party",
					image: nyc_3
				},
				{
					caption: "Brooklyn Half Marathon",
					image: nyc_4
				},
			]
		},
		{
			date: "January 2025",
			title: "Will you marry me?",
			description: "Gabe proposed to Elyse at the first summit of their hiking trip in Chilean Patagonia. Queue an exciting year of travel, job changes, and preparing for the biggest day of our lives!",
			photos: [
				{
					image: proposal_1
				},
				{
					image: proposal_2
				},
				{
					image: proposal_3
				},
			]
		},
		{
			date: "August 2026",
			title: "Our Wedding Day",
			description: "The day we've been dreaming of - celebrating our love with all our favorite people in the beautiful mountains of North Carolina."
		}
	];

	// Slideshow state for each timeline event
	let slideshowStates = $state(timelineEvents.map(() => ({ currentIndex: 0 })));

	function nextSlide(eventIndex: number, photoCount: number) {
		slideshowStates[eventIndex].currentIndex = (slideshowStates[eventIndex].currentIndex + 1) % photoCount;
	}

	function prevSlide(eventIndex: number, photoCount: number) {
		slideshowStates[eventIndex].currentIndex = slideshowStates[eventIndex].currentIndex === 0 
			? photoCount - 1 
			: slideshowStates[eventIndex].currentIndex - 1;
	}

	function goToSlide(eventIndex: number, slideIndex: number) {
		slideshowStates[eventIndex].currentIndex = slideIndex;
	}

	// Touch/swipe handling
	let touchStartX = 0;
	let touchEndX = 0;

	function handleTouchStart(e: TouchEvent) {
		touchStartX = e.changedTouches[0].screenX;
	}

	function handleTouchEnd(e: TouchEvent, eventIndex: number, photoCount: number) {
		touchEndX = e.changedTouches[0].screenX;
		handleSwipe(eventIndex, photoCount);
	}

	function handleSwipe(eventIndex: number, photoCount: number) {
		const swipeThreshold = 50;
		const swipeDistance = touchStartX - touchEndX;
		
		if (Math.abs(swipeDistance) > swipeThreshold) {
			if (swipeDistance > 0) {
				// Swipe left - next slide
				nextSlide(eventIndex, photoCount);
			} else {
				// Swipe right - previous slide
				prevSlide(eventIndex, photoCount);
			}
		}
	}
</script>

<svelte:head>
	<title>Our Story - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white pb-20">
	<div class="w-full bg-cover bg-center py-24 mb-12" style="background-image: linear-gradient(rgba(0,0,0,0.35), rgba(0,0,0,0.35)), url('/our-story/background.jpeg');">
		<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
			<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-white tracking-wider mb-6">
				Our Story
			</h1>
			<div class="w-24 h-px bg-white mx-auto mb-8"></div>
			<p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto">
				Every love story is beautiful, but ours is our favorite. Here's how our journey began and where it's taking us.
			</p>
		</div>
	</div>
</section>

<!-- Timeline Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="relative">
			<!-- Timeline Line -->
			<div class="absolute left-8 md:left-1/2 transform md:-translate-x-0.5 top-0 bottom-0 w-0.5 bg-gray-300"></div>
			
			{#each timelineEvents as event, index}
				<div class="relative flex items-center mb-12 md:mb-16">
					<!-- Timeline Dot -->
					<div class="absolute left-6 md:left-1/2 transform md:-translate-x-1/2 w-4 h-4 bg-black rounded-full border-4 border-white shadow-sm z-10"></div>
					
					<!-- Content -->
					<div class="ml-16 md:ml-0 md:w-1/2 {index % 2 === 0 ? 'md:pr-12' : 'md:pl-12 md:ml-auto'}">
						<div class="bg-white rounded-lg shadow-sm border border-gray-100 overflow-hidden">
							<!-- Photo slideshow if photos exist -->
							{#if event.photos && event.photos.length > 0}
								<!-- 4:3 — a bit taller than 7:5 for more vertical room -->
								<div class="relative aspect-[4/3] bg-white">
									<!-- Slideshow container -->
									<div 
										class="relative h-full w-full overflow-hidden bg-white"
										ontouchstart={handleTouchStart}
										ontouchend={(e) => handleTouchEnd(e, index, event.photos?.length || 0)}
									>
										<!-- Photo slides: full container height; narrower images get black side bars, wider images are center-cropped -->
										{#each event.photos as photo, photoIndex}
											<div
												class="absolute inset-0 flex items-center justify-center overflow-hidden bg-white transition-transform duration-300 ease-in-out {photoIndex === slideshowStates[index].currentIndex ? 'translate-x-0' : photoIndex < slideshowStates[index].currentIndex ? '-translate-x-full' : 'translate-x-full'}"
											>
												<img
													src={photo.image}
													alt={photo.caption}
													class="h-full w-auto max-w-none shrink-0 select-none"
													draggable="false"
												/>
											</div>
										{/each}
									</div>

									<!-- Photo caption (always on top of photo) -->
									{#if event.photos[slideshowStates[index].currentIndex].caption}
										<div class="pointer-events-none absolute top-2 left-2 z-10 bg-gray-400/80 text-white text-xs px-2 py-1 rounded max-w-[calc(100%-1rem)]">
											{event.photos[slideshowStates[index].currentIndex].caption}
										</div>
									{/if}

									<!-- Photo counter (only when multiple photos) -->
									{#if event.photos.length > 1}
										<div class="pointer-events-none absolute top-2 right-2 z-10 bg-gray-400/80 text-white text-xs px-2 py-1 rounded">
											{slideshowStates[index].currentIndex + 1} / {event.photos.length}
										</div>
									{/if}

									<!-- Navigation arrows (only show if more than 1 photo) -->
									{#if event.photos.length > 1}
										<button 
											class="absolute left-2 top-1/2 transform -translate-y-1/2 z-10 bg-gray-400 bg-opacity-70 hover:bg-opacity-90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer"
											onclick={() => prevSlide(index, event.photos?.length || 0)}
											aria-label="Previous photo"
										>
											<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
											</svg>
										</button>
										<button 
											class="absolute right-2 top-1/2 transform -translate-y-1/2 z-10 bg-gray-400 bg-opacity-70 hover:bg-opacity-90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer"
											onclick={() => nextSlide(index, event.photos?.length || 0)}
											aria-label="Next photo"
										>
											<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
											</svg>
										</button>
									{/if}
								</div>
							{/if}
							<div class="p-6">
								<div class="text-sm text-gray-500 mb-2 font-light tracking-wide">{event.date}</div>
								<h3 class="text-xl font-light text-black mb-3">{event.title}</h3>
								<p class="text-gray-600 leading-relaxed">{event.description}</p>
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Quote Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<blockquote class="text-2xl sm:text-3xl font-light text-black italic mb-8">
			"In all the world, there is no heart for me like yours. In all the world, there is no love for you like mine."
		</blockquote>
		<cite class="text-gray-500">— Maya Angelou</cite>
	</div>
</section>
