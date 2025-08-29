<script lang="ts">
	interface Hotel {
		name: string;
		address: string;
		phone: string;
		website: string;
		description: string;
		distance: string;
		priceRange: string;
	}

	const recommendedHotels: Hotel[] = [
		{
			name: "The Greystone Inn",
			address: "Greystone Lane, Lake Toxaway, NC 28747",
			phone: "(828) 966-4700",
			website: "greystoneinn.com",
			description: "A luxury lakeside resort offering elegant accommodations with stunning mountain views. Perfect for a special weekend getaway.",
			distance: "15 minutes from venue",
			priceRange: "$$$"
		},
		{
			name: "Cashiers Mountain Lodge",
			address: "Highway 107 South, Cashiers, NC 28717", 
			phone: "(828) 743-4446",
			website: "cashiersmountainlodge.com",
			description: "Cozy mountain lodge with comfortable rooms and easy access to hiking trails and local attractions.",
			distance: "5 minutes from venue",
			priceRange: "$$"
		},
		{
			name: "High Hampton Resort",
			address: "1525 Highway 107 South, Cashiers, NC 28717",
			phone: "(828) 743-2411", 
			website: "highhamptonresort.com",
			description: "Historic mountain resort with golf course, spa services, and beautiful lake views. Great for families.",
			distance: "10 minutes from venue",
			priceRange: "$$$"
		},
		{
			name: "Hampton Inn & Suites Cashiers",
			address: "201 Highway 107 North, Cashiers, NC 28717",
			phone: "(828) 743-5500",
			website: "hilton.com",
			description: "Modern hotel with complimentary breakfast and indoor pool. Reliable comfort with all the amenities.",
			distance: "8 minutes from venue",
			priceRange: "$$"
		}
	];
</script>

<svelte:head>
	<title>Travel - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Travel
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			Everything you need to know about getting to Cashiers, North Carolina and where to stay for our wedding weekend.
		</p>
	</div>
</section>

<!-- Getting There Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="text-center mb-16">
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Getting There</h2>
			<div class="w-24 h-px bg-black mx-auto"></div>
		</div>

		<div class="grid md:grid-cols-3 gap-12">
			<!-- By Air -->
			<div class="text-center">
				<div class="w-16 h-16 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-sm">
					<svg class="w-8 h-8 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"></path>
					</svg>
				</div>
				<h3 class="text-xl font-light text-black mb-4">By Air</h3>
				<div class="text-left bg-white p-6 rounded-lg">
					<div class="mb-4">
						<p class="font-medium text-black mb-1">Asheville Regional Airport (AVL)</p>
						<p class="text-sm text-gray-600">1 hour drive • Most convenient</p>
					</div>
					<div class="mb-4">
						<p class="font-medium text-black mb-1">Greenville-Spartanburg (GSP)</p>
						<p class="text-sm text-gray-600">1.5 hour drive • Good flight options</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">Charlotte Douglas (CLT)</p>
						<p class="text-sm text-gray-600">2.5 hour drive • Major hub</p>
					</div>
				</div>
			</div>

			<!-- By Car -->
			<div class="text-center">
				<div class="w-16 h-16 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-sm">
					<svg class="w-8 h-8 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"></path>
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 6h1l1 7H9l1-7h3zM5 17h14l-1-7H6l-1 7z"></path>
					</svg>
				</div>
				<h3 class="text-xl font-light text-black mb-4">By Car</h3>
				<div class="text-left bg-white p-6 rounded-lg">
					<div class="mb-4">
						<p class="font-medium text-black mb-1">From Atlanta</p>
						<p class="text-sm text-gray-600">2.5 hours via I-85 & US-441</p>
					</div>
					<div class="mb-4">
						<p class="font-medium text-black mb-1">From Charlotte</p>
						<p class="text-sm text-gray-600">2.5 hours via I-85 & US-64</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">From Greenville</p>
						<p class="text-sm text-gray-600">1.5 hours via US-276</p>
					</div>
				</div>
			</div>

			<!-- Parking -->
			<div class="text-center">
				<div class="w-16 h-16 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-sm">
					<svg class="w-8 h-8 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
					</svg>
				</div>
				<h3 class="text-xl font-light text-black mb-4">Parking & Shuttles</h3>
				<div class="text-left bg-white p-6 rounded-lg">
					<div class="mb-4">
						<p class="font-medium text-black mb-1">Free Parking</p>
						<p class="text-sm text-gray-600">Available at the venue</p>
					</div>
					<div class="mb-4">
						<p class="font-medium text-black mb-1">Shuttle Service</p>
						<p class="text-sm text-gray-600">From recommended hotels</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">Ride Share</p>
						<p class="text-sm text-gray-600">Uber & Lyft available</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Accommodations Section -->
<section class="bg-white py-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="text-center mb-16">
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Where to Stay</h2>
			<div class="w-24 h-px bg-black mx-auto mb-6"></div>
			<p class="text-lg text-gray-600 max-w-2xl mx-auto">
				We've reserved room blocks at these hotels. Book early for the best rates and availability!
			</p>
		</div>

		<div class="grid lg:grid-cols-2 gap-8">
			{#each recommendedHotels as hotel}
				<div class="bg-gray-50 p-8 rounded-lg">
					<div class="flex justify-between items-start mb-4">
						<h3 class="text-xl font-light text-black">{hotel.name}</h3>
						<span class="text-sm text-gray-500">{hotel.priceRange}</span>
					</div>
					
					<p class="text-gray-600 mb-4 leading-relaxed">{hotel.description}</p>
					
					<div class="space-y-2 text-sm">
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
							</svg>
							{hotel.distance}
						</div>
						
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
							</svg>
							{hotel.phone}
						</div>
						
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9v-9m0-9v9"></path>
							</svg>
							{hotel.website}
						</div>
					</div>
					
					<button class="mt-6 w-full px-4 py-2 border border-black text-black hover:bg-black hover:text-white transition-colors duration-200 font-light tracking-wide">
						Book Now
					</button>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Local Transportation -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Local Transportation</h2>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		
		<div class="grid md:grid-cols-2 gap-8">
			<div class="bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-3">Rental Cars</h3>
				<p class="text-gray-600 text-sm mb-4">Available at all airports. Recommended for exploring the area and flexibility.</p>
				<p class="text-xs text-gray-500">Book early for better rates</p>
			</div>
			
			<div class="bg-white p-6 rounded-lg">
				<h3 class="text-lg font-light text-black mb-3">Ride Share</h3>
				<p class="text-gray-600 text-sm mb-4">Uber and Lyft operate in the area, though availability may be limited in remote areas.</p>
				<p class="text-xs text-gray-500">Plan extra time for pickup</p>
			</div>
		</div>
		
		<div class="mt-12 bg-white p-8 rounded-lg">
			<h3 class="text-lg font-light text-black mb-4">Need Help Planning?</h3>
			<p class="text-gray-600 mb-4">If you need assistance with travel arrangements or have questions about the area, don't hesitate to reach out to us!</p>
			<p class="text-sm text-gray-500">We're happy to help make your trip as smooth as possible.</p>
		</div>
	</div>
</section>
