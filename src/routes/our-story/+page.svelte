<script lang="ts">
	interface TimelineEvent {
		date: string;
		title: string;
		description: string;
		image?: string;
		imageDescription?: string;
	}

	const timelineEvents: TimelineEvent[] = [
		{
			date: "Spring 2018",
			title: "First Meeting",
			description: "We first met at a mutual friend's party in college. Gabriel was immediately drawn to Elyse's infectious laugh, while Elyse was charmed by Gabriel's witty sense of humor.",
			imageDescription: "A candid photo from the college party where we first met"
		},
		{
			date: "Summer 2018",
			title: "First Date",
			description: "Our first official date was a picnic in the park followed by a walk along the river. We talked for hours about our dreams, aspirations, and favorite movies.",
			imageDescription: "Our picnic setup in the park - still have this blanket!"
		},
		{
			date: "Fall 2018",
			title: "Becoming Official",
			description: "After months of getting to know each other, we made it official. Gabriel asked Elyse to be his girlfriend during a beautiful autumn evening walk."
		},
		{
			date: "Summer 2019",
			title: "First Trip Together",
			description: "Our first vacation together was a road trip to the mountains. We discovered our shared love for hiking, stargazing, and trying new foods.",
			imageDescription: "Summit photo from our first hiking adventure together"
		},
		{
			date: "Spring 2020",
			title: "Moving In Together",
			description: "Despite the challenges of the pandemic, we decided to move in together. It was the best decision we ever made, and we grew even closer during this time.",
			imageDescription: "Surrounded by moving boxes in our first apartment"
		},
		{
			date: "Fall 2021",
			title: "Adopting Luna",
			description: "We welcomed our furry daughter Luna into our lives. This sweet rescue dog completed our little family and brought us so much joy.",
			imageDescription: "Luna's first day home - she immediately claimed the couch"
		},
		{
			date: "Summer 2023",
			title: "Cross-Country Adventure",
			description: "We embarked on an epic cross-country road trip, visiting national parks and creating memories that will last a lifetime.",
			imageDescription: "Our road trip map with all the national parks we visited"
		},
		{
			date: "December 2024",
			title: "The Proposal",
			description: "Gabriel proposed during a winter hike to our favorite overlook. With the snow falling gently around us, he got down on one knee and asked Elyse to be his forever.",
			imageDescription: "The moment right after 'Yes!' - tears of joy in the snow"
		},
		{
			date: "August 2026",
			title: "Our Wedding Day",
			description: "The day we've been dreaming of - celebrating our love with all our favorite people in the beautiful mountains of North Carolina."
		}
	];
</script>

<svelte:head>
	<title>Our Story - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Our Story
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			Every love story is beautiful, but ours is our favorite. Here's how our journey began and where it's taking us.
		</p>
	</div>
</section>

<!-- Timeline Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
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
							<!-- Photo placeholder if image description exists -->
							{#if event.imageDescription}
								<div class="aspect-video bg-gray-100 flex items-center justify-center border-b border-gray-100">
									<div class="text-center p-6">
										<svg class="w-8 h-8 text-gray-400 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
											<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
										</svg>
										<p class="text-xs text-gray-500 text-center">{event.imageDescription}</p>
									</div>
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

<!-- Fun Facts Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="text-center mb-16">
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Fun Facts About Us</h2>
			<div class="w-24 h-px bg-black mx-auto"></div>
		</div>

		<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">First Dance Song</h3>
				<p class="text-gray-600">"Perfect" by Ed Sheeran</p>
			</div>
			
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">Favorite Date Night</h3>
				<p class="text-gray-600">Cooking dinner together at home</p>
			</div>
			
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">Dream Honeymoon</h3>
				<p class="text-gray-600">Safari in Kenya</p>
			</div>
			
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">Shared Hobby</h3>
				<p class="text-gray-600">Hiking and photography</p>
			</div>
			
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">Years Together</h3>
				<p class="text-gray-600">8 amazing years</p>
			</div>
			
			<div class="text-center bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-2">Favorite Memory</h3>
				<p class="text-gray-600">Watching the sunrise from our tent</p>
			</div>
		</div>
	</div>
</section>
