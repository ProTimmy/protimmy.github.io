<script lang="ts">
	interface Activity {
		name: string;
		category: string;
		description: string;
		location: string;
		duration: string;
		difficulty?: string;
		season?: string;
		website?: string;
	}

	const activities: Activity[] = [
		{
			name: "Whiteside Mountain Trail",
			category: "Hiking",
			description: "A moderate 2-mile loop trail offering spectacular panoramic views of the surrounding mountains and valleys. One of the most popular hikes in the area.",
			location: "Highlands-Cashiers Road",
			duration: "1.5-2 hours",
			difficulty: "Moderate",
			season: "Year-round"
		},
		{
			name: "Looking Glass Falls",
			category: "Nature",
			description: "A stunning 60-foot waterfall that you can walk behind. Easily accessible with a short walk from the parking area.",
			location: "Blue Ridge Parkway",
			duration: "30 minutes",
			difficulty: "Easy",
			season: "Year-round"
		},
		{
			name: "Cashiers Farmers Market",
			category: "Shopping",
			description: "Local farmers market featuring fresh produce, artisanal crafts, and regional specialties. Great for unique souvenirs.",
			location: "Downtown Cashiers",
			duration: "1-2 hours",
			season: "May-October, Saturdays"
		},
		{
			name: "High Hampton Resort Golf",
			category: "Recreation",
			description: "18-hole championship golf course set in the beautiful Blue Ridge Mountains. Challenging course with stunning views.",
			location: "High Hampton Resort",
			duration: "4-5 hours",
			season: "April-October",
			website: "highhamptonresort.com"
		},
		{
			name: "Cullasaja Falls",
			category: "Nature",
			description: "A beautiful 250-foot cascading waterfall visible from the road, with hiking trails for closer views.",
			location: "US Highway 64",
			duration: "30 minutes - 2 hours",
			difficulty: "Easy to Moderate",
			season: "Year-round"
		},
		{
			name: "Village Green Antique Mall",
			category: "Shopping",
			description: "Large antique mall with multiple vendors offering everything from vintage furniture to collectibles and local crafts.",
			location: "Cashiers Village",
			duration: "1-3 hours",
			season: "Year-round"
		},
		{
			name: "Panthertown Valley",
			category: "Hiking",
			description: "Known as the 'Yosemite of the East' with granite domes, waterfalls, and pristine wilderness. Multiple trail options.",
			location: "Panthertown Valley",
			duration: "2-6 hours",
			difficulty: "Moderate to Difficult",
			season: "Year-round"
		},
		{
			name: "Cashiers Lake",
			category: "Recreation",
			description: "Private lake perfect for kayaking, fishing, or just enjoying a peaceful lakeside picnic. Rentals available.",
			location: "Cashiers Lake Road",
			duration: "2-4 hours",
			season: "May-September"
		},
		{
			name: "The Ugly Dog Public House",
			category: "Dining",
			description: "Popular local restaurant known for great burgers, craft beer, and live music. Casual mountain atmosphere.",
			location: "Downtown Cashiers",
			duration: "1-2 hours",
			season: "Year-round"
		},
		{
			name: "Sapphire Valley Ski Area",
			category: "Recreation",
			description: "Small ski resort perfect for beginners and families. Also offers tubing and other winter activities.",
			location: "Sapphire, NC",
			duration: "Half or full day",
			season: "December-March"
		},
		{
			name: "Cashiers Designer Outlets",
			category: "Shopping",
			description: "Outlet shopping with popular brands at discounted prices. Good for rainy day activities.",
			location: "US Highway 64",
			duration: "2-4 hours",
			season: "Year-round"
		},
		{
			name: "Blue Ridge Parkway Scenic Drive",
			category: "Sightseeing",
			description: "One of America's most beautiful drives with numerous overlooks, hiking trails, and picnic areas.",
			location: "Various access points",
			duration: "2-8 hours",
			season: "Year-round (weather permitting)"
		}
	];

	const categories = ['All', 'Hiking', 'Nature', 'Shopping', 'Recreation', 'Dining', 'Sightseeing'];
	let selectedCategory = $state('All');

	let filteredActivities = $derived(selectedCategory === 'All' 
		? activities 
		: activities.filter(activity => activity.category === selectedCategory));

	function selectCategory(category: string) {
		selectedCategory = category;
	}
</script>

<svelte:head>
	<title>Things to Do - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Things to Do
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			Make the most of your visit to the beautiful Cashiers area with our recommendations for activities, dining, and attractions.
		</p>
	</div>
</section>

<!-- Filter Section -->
<section class="bg-gray-50 py-12">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex flex-wrap justify-center gap-4">
			{#each categories as category}
				<button
					onclick={() => selectCategory(category)}
					class="px-6 py-2 text-sm font-light tracking-wide transition-colors duration-200 {selectedCategory === category 
						? 'bg-black text-white' 
						: 'bg-white text-black border border-gray-200 hover:border-black'}"
				>
					{category}
				</button>
			{/each}
		</div>
	</div>
</section>

<!-- Activities Grid -->
<section class="bg-gray-50 pb-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="grid lg:grid-cols-2 gap-6">
			{#each filteredActivities as activity}
				<div class="bg-white p-6 rounded-lg shadow-sm hover:shadow-md transition-shadow duration-200">
					<div class="flex justify-between items-start mb-3">
						<h3 class="text-xl font-light text-black">{activity.name}</h3>
						<span class="text-xs text-gray-500 bg-gray-100 px-2 py-1 rounded">{activity.category}</span>
					</div>
					
					<p class="text-gray-600 mb-4 leading-relaxed">{activity.description}</p>
					
					<div class="space-y-2 text-sm">
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
							</svg>
							<span>{activity.location}</span>
						</div>
						
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
							</svg>
							<span>{activity.duration}</span>
						</div>
						
						{#if activity.difficulty}
							<div class="flex items-center text-gray-600">
								<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
								</svg>
								<span>{activity.difficulty}</span>
							</div>
						{/if}
						
						{#if activity.season}
							<div class="flex items-center text-gray-600">
								<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
								</svg>
								<span>{activity.season}</span>
							</div>
						{/if}
						
						{#if activity.website}
							<div class="flex items-center text-gray-600">
								<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9v-9m0-9v9"></path>
								</svg>
								<span>{activity.website}</span>
							</div>
						{/if}
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Local Tips Section -->
<section class="bg-white py-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="text-center mb-16">
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Local Tips</h2>
			<div class="w-24 h-px bg-black mx-auto"></div>
		</div>

		<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
			<div class="text-center bg-gray-50 p-6 rounded-lg">
				<div class="w-12 h-12 bg-white rounded-full flex items-center justify-center mx-auto mb-4">
					<svg class="w-6 h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z"></path>
					</svg>
				</div>
				<h3 class="text-lg font-light text-black mb-2">Weather</h3>
				<p class="text-gray-600 text-sm">Mountain weather can change quickly. Layer up and bring a rain jacket!</p>
			</div>
			
			<div class="text-center bg-gray-50 p-6 rounded-lg">
				<div class="w-12 h-12 bg-white rounded-full flex items-center justify-center mx-auto mb-4">
					<svg class="w-6 h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
					</svg>
				</div>
				<h3 class="text-lg font-light text-black mb-2">Cell Service</h3>
				<p class="text-gray-600 text-sm">Service can be spotty in remote areas. Download offline maps before heading out.</p>
			</div>
			
			<div class="text-center bg-gray-50 p-6 rounded-lg">
				<div class="w-12 h-12 bg-white rounded-full flex items-center justify-center mx-auto mb-4">
					<svg class="w-6 h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"></path>
					</svg>
				</div>
				<h3 class="text-lg font-light text-black mb-2">Cash</h3>
				<p class="text-gray-600 text-sm">Some local businesses prefer cash. ATMs are available but not everywhere.</p>
			</div>
		</div>
	</div>
</section>

<!-- Contact Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Need More Recommendations?</h2>
		<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
			We love this area and have spent lots of time exploring! If you need specific recommendations or have questions about any of these activities, just ask.
		</p>
		<div class="bg-white p-8 rounded-lg">
			<p class="text-gray-600 mb-4">We're happy to help you plan the perfect weekend!</p>
			<p class="text-sm text-gray-500">Reach out to us at <span class="text-black">hello@gabrielandelyse.com</span></p>
		</div>
	</div>
</section>
