<script lang="ts">
	interface Hotel {
		name: string;
		address: string;
		phone: string;
		website: string;
		description: string;
		distance: string;
		images: string[];
	}

	const featuredHotel: Hotel = {
		name: "Hampton Inn & Suites Cashiers",
		address: "201 Highway 107 North, Cashiers, NC 28717",
		phone: "(828) 743-5500",
		website: "https://www.hilton.com/en/hotels/casnchx-hampton-suites-cashiers-sapphire-valley/",
		description: "Modern hotel with complimentary breakfast and indoor pool. Reliable comfort with all the amenities.",
		distance: "8 minutes from venue",
		images: ["/travel/hampton-inn-1.avif", "/travel/hampton-inn-2.avif", "/travel/hampton-inn-3.jpg"]
	};

	const otherHotels: Hotel[] = [
		{
			name: "Hotel Cashiers",
			address: "7 Slab Town Road, Cashiers, NC  28717",
			phone: "(828) 743-7706",
			website: "hotelcashiers.com",
			description: "A boutique hotel nestled in the charming mountain village of Cashiers, offering a refined yet relaxed retreat with well-appointed rooms and proximity to local shopping and dining.",
			distance: "5 minutes from venue",
			images: ["/travel/hotel-cashiers-1.webp", "/travel/hotel-cashiers-2.avif", "/travel/hotel-cashiers-3.jpg"]
		},
		{
			name: "The Wells Hotel",
			address: "58 NC-107, Cashiers, NC 28717",
			phone: "(828) 761-6289",
			website: "thewellscashiers.com",
			description: "A charming boutique hotel in the heart of Cashiers, featuring an on-site brewery and a relaxed mountain atmosphere.",
			distance: "5 minutes from venue",
			images: ["/travel/the-wells-hotel-1.jpg", "/travel/the-wells-hotel-2.jpg", "/travel/the-wells-hotel-3.jpg"]
		},
		{
			name: "High Hampton Resort",
			address: "1525 Highway 107 South, Cashiers, NC 28717",
			phone: "(828) 743-2411",
			website: "highhamptonresort.com",
			description: "Historic mountain resort with golf course, spa services, and beautiful lake views. Great for families.",
			distance: "10 minutes from venue",
			images: ["/travel/high-hampton-resort-1.webp", "/travel/high-hampton-resort-2.webp", "/travel/high-hampton-resort-3.jpg"]
		}
	];

	const allHotels = [featuredHotel, ...otherHotels];
	let slideshowStates = $state(allHotels.map(() => ({ currentIndex: 0 })));

	function nextSlide(hotelIndex: number, count: number) {
		slideshowStates[hotelIndex].currentIndex = (slideshowStates[hotelIndex].currentIndex + 1) % count;
	}

	function prevSlide(hotelIndex: number, count: number) {
		slideshowStates[hotelIndex].currentIndex =
			slideshowStates[hotelIndex].currentIndex === 0
				? count - 1
				: slideshowStates[hotelIndex].currentIndex - 1;
	}

	function websiteUrl(website: string) {
		return website.startsWith('http') ? website : `https://${website}`;
	}

	function phoneHref(phone: string) {
		return `tel:${phone.replace(/\D/g, '')}`;
	}

	let touchStartX = 0;
	let touchEndX = 0;

	function handleTouchStart(e: TouchEvent) {
		touchStartX = e.changedTouches[0].screenX;
	}

	function handleTouchEnd(e: TouchEvent, hotelIndex: number, count: number) {
		touchEndX = e.changedTouches[0].screenX;
		const swipeDistance = touchStartX - touchEndX;
		if (Math.abs(swipeDistance) > 50) {
			if (swipeDistance > 0) nextSlide(hotelIndex, count);
			else prevSlide(hotelIndex, count);
		}
	}
</script>

<svelte:head>
	<title>Travel - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white pb-20">
	<div class="w-full bg-cover bg-center py-24 mb-12" style="background-image: linear-gradient(rgba(0,0,0,0.35), rgba(0,0,0,0.35)), url('/travel/background.png');">
		<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
			<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-white tracking-wider mb-6">
				Travel
			</h1>
			<div class="w-24 h-px bg-white mx-auto mb-8"></div>
			<p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto">
				Everything you need to know about getting to Cashiers, North Carolina and where to stay for our wedding weekend.
			</p>
		</div>
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
						<p class="text-sm text-gray-600">1.5 hour drive • Most convenient</p>
					</div>
					<div class="mb-4">
						<p class="font-medium text-black mb-1">Charlotte Douglas (CLT)</p>
						<p class="text-sm text-gray-600">3 hour drive • Major hub</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">Hartsfield-Jackson Atlanta (ATL)</p>
						<p class="text-sm text-gray-600">3 hour drive • Major hub</p>
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
						<p class="font-medium text-black mb-1">From Asheville</p>
						<p class="text-sm text-gray-600">1.5 hours via US-64</p>
					</div>
					<div class="mb-4">
						<p class="font-medium text-black mb-1">From Atlanta</p>
						<p class="text-sm text-gray-600">3 hours via I-85 & US-441</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">From Charlotte</p>
						<p class="text-sm text-gray-600">3 hours via I-85 & US-64</p>
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
						<p class="text-sm text-gray-600">From Hampton Inn Hotel</p>
					</div>
					<div>
						<p class="font-medium text-black mb-1">Ride Share</p>
						<p class="text-sm text-gray-600">Uber available</p>
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
				We recommend staying at our hotel block or one of the nearby options below.
			</p>
		</div>

		<!-- Featured Hotel Block -->
		<div class="mb-16">
			<div class="text-center mb-8">
				<span class="inline-block border border-black text-black text-xs tracking-widest uppercase px-4 py-1.5 mb-4">Our Hotel Block</span>
				<p class="text-sm text-gray-500 max-w-xl mx-auto">We are securing a room block at this hotel. More details on booking the block coming soon — in the meantime, feel free to reach out to us with any questions.</p>
			</div>
			<div class="max-w-2xl mx-auto bg-gray-50 border border-black rounded-lg overflow-hidden">
				<!-- Slideshow -->
				<div class="relative aspect-[4/3] bg-gray-200">
					<div
						class="relative h-full w-full overflow-hidden"
						ontouchstart={handleTouchStart}
						ontouchend={(e) => handleTouchEnd(e, 0, featuredHotel.images.length)}
					>
						{#each featuredHotel.images as image, photoIndex}
							<div class="absolute inset-0 flex items-center justify-center overflow-hidden bg-gray-200 transition-transform duration-300 ease-in-out {photoIndex === slideshowStates[0].currentIndex ? 'translate-x-0' : photoIndex < slideshowStates[0].currentIndex ? '-translate-x-full' : 'translate-x-full'}">
								<img src={image} alt={featuredHotel.name} class="h-full w-auto max-w-none shrink-0 select-none" draggable="false" />
							</div>
						{/each}
					</div>
					{#if featuredHotel.images.length > 1}
						<div class="pointer-events-none absolute top-2 right-2 z-10 bg-gray-400/80 text-white text-xs px-2 py-1 rounded">
							{slideshowStates[0].currentIndex + 1} / {featuredHotel.images.length}
						</div>
						<button class="absolute left-2 top-1/2 -translate-y-1/2 z-10 bg-gray-400/70 hover:bg-gray-400/90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer" onclick={() => prevSlide(0, featuredHotel.images.length)} aria-label="Previous photo">
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
						</button>
						<button class="absolute right-2 top-1/2 -translate-y-1/2 z-10 bg-gray-400/70 hover:bg-gray-400/90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer" onclick={() => nextSlide(0, featuredHotel.images.length)} aria-label="Next photo">
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
						</button>
					{/if}
				</div>
				<div class="p-8">
					<h3 class="text-2xl font-bold text-black mb-4">{featuredHotel.name}</h3>
					<p class="text-gray-600 mb-4 leading-relaxed">{featuredHotel.description}</p>
					<div class="space-y-2 text-sm">
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
							</svg>
							{featuredHotel.distance}
						</div>
						<div class="flex items-center text-gray-600">
							<svg class="w-4 h-4 mr-2 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
							</svg>
							<a href={phoneHref(featuredHotel.phone)} class="text-sky-500 hover:text-sky-700 md:pointer-events-none">{featuredHotel.phone}</a>
						</div>
					</div>
					<a href={websiteUrl(featuredHotel.website)} target="_blank" rel="noopener noreferrer" class="mt-6 block w-full px-4 py-2 bg-black text-white hover:bg-gray-800 transition-colors duration-200 font-light tracking-wide cursor-pointer text-center">
						Book Now
					</a>
					<p class="mt-4 text-xs text-gray-500 leading-relaxed">
						*Guests phoning should mention: <b>Armstrong Timotei Wedding - 7.31.26 - 3nts</b>
					</p>
					<p class="mt-4 text-xs text-gray-500 leading-relaxed">
						Reservations by attendees must be received on or before 6/30/26. On this date, HGV will review the reservation pick up for the event and release any unreserved rooms from this room block for general sale. Additional rooms requested above the contracted amount, will be based upon rate and room availability.
					</p>
				</div>
			</div>
		</div>

		<!-- Other Hotels -->
		<div>
			<div class="text-center mb-8">
				<h3 class="text-xl font-light text-black mb-2">Additional Options</h3>
				<div class="w-16 h-px bg-gray-300 mx-auto"></div>
			</div>
			<div class="grid lg:grid-cols-3 gap-8">
				{#each otherHotels as hotel, i}
					{@const hotelIndex = i + 1}
					<div class="bg-gray-50 rounded-lg overflow-hidden border border-black flex flex-col">
						<!-- Slideshow -->
						<div class="relative aspect-[4/3] bg-gray-200">
							<div
								class="relative h-full w-full overflow-hidden"
								ontouchstart={handleTouchStart}
								ontouchend={(e) => handleTouchEnd(e, hotelIndex, hotel.images.length)}
							>
								{#each hotel.images as image, photoIndex}
									<div class="absolute inset-0 flex items-center justify-center overflow-hidden bg-gray-200 transition-transform duration-300 ease-in-out {photoIndex === slideshowStates[hotelIndex].currentIndex ? 'translate-x-0' : photoIndex < slideshowStates[hotelIndex].currentIndex ? '-translate-x-full' : 'translate-x-full'}">
										<img src={image} alt={hotel.name} class="h-full w-auto max-w-none shrink-0 select-none" draggable="false" />
									</div>
								{/each}
							</div>
							{#if hotel.images.length > 1}
								<div class="pointer-events-none absolute top-2 right-2 z-10 bg-gray-400/80 text-white text-xs px-2 py-1 rounded">
									{slideshowStates[hotelIndex].currentIndex + 1} / {hotel.images.length}
								</div>
								<button class="absolute left-2 top-1/2 -translate-y-1/2 z-10 bg-gray-400/70 hover:bg-gray-400/90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer" onclick={() => prevSlide(hotelIndex, hotel.images.length)} aria-label="Previous photo">
									<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
								</button>
								<button class="absolute right-2 top-1/2 -translate-y-1/2 z-10 bg-gray-400/70 hover:bg-gray-400/90 text-white p-1 rounded-full transition-all duration-200 cursor-pointer" onclick={() => nextSlide(hotelIndex, hotel.images.length)} aria-label="Next photo">
									<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
								</button>
							{/if}
						</div>
						<div class="p-8 flex flex-col flex-1">
							<h3 class="text-xl font-bold text-black mb-4">{hotel.name}</h3>
							<p class="text-gray-600 mb-4 leading-relaxed">{hotel.description}</p>
							<div class="space-y-2 text-sm mb-6">
								<div class="flex items-center text-gray-600">
									<svg class="w-4 h-4 mr-2 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
									</svg>
									{hotel.distance}
								</div>
								<div class="flex items-center text-gray-600">
									<svg class="w-4 h-4 mr-2 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
									</svg>
									<a href={phoneHref(hotel.phone)} class="text-sky-500 hover:text-sky-700 md:pointer-events-none">{hotel.phone}</a>
								</div>
							</div>
								<a href={websiteUrl(hotel.website)} target="_blank" rel="noopener noreferrer" class="mt-auto block w-full px-4 py-2 border border-black text-black hover:bg-black hover:text-white transition-colors duration-200 font-light tracking-wide cursor-pointer text-center">
									Book Now
								</a>
							</div>
						</div>
					{/each}
			</div>
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
				<p class="text-gray-600 text-sm mb-4">Uber operates in the area, though availability may be limited in remote areas.</p>
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
