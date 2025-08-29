<script lang="ts">
	interface Photo {
		id: number;
		title: string;
		category: string;
		placeholder: string;
	}

	const photoCategories = [
		'All',
		'Engagement',
		'Travel',
		'Everyday Moments',
		'Family & Friends'
	];

	const photos: Photo[] = [
		{ id: 1, title: 'Engagement Shoot', category: 'Engagement', placeholder: 'Beautiful engagement photo in the mountains' },
		{ id: 2, title: 'Proposal Moment', category: 'Engagement', placeholder: 'The moment Gabriel proposed' },
		{ id: 3, title: 'Road Trip Adventure', category: 'Travel', placeholder: 'Cross-country road trip memories' },
		{ id: 4, title: 'Hiking Together', category: 'Travel', placeholder: 'Exploring nature trails' },
		{ id: 5, title: 'Cooking at Home', category: 'Everyday Moments', placeholder: 'Sunday morning breakfast prep' },
		{ id: 6, title: 'Movie Night', category: 'Everyday Moments', placeholder: 'Cozy night in watching movies' },
		{ id: 7, title: 'With Luna', category: 'Everyday Moments', placeholder: 'Playing with our rescue dog' },
		{ id: 8, title: 'Family Gathering', category: 'Family & Friends', placeholder: 'Thanksgiving dinner with family' },
		{ id: 9, title: 'Friends Weekend', category: 'Family & Friends', placeholder: 'Weekend getaway with friends' },
		{ id: 10, title: 'Beach Vacation', category: 'Travel', placeholder: 'Sunset walk on the beach' },
		{ id: 11, title: 'Date Night', category: 'Everyday Moments', placeholder: 'Dinner at our favorite restaurant' },
		{ id: 12, title: 'Engagement Party', category: 'Engagement', placeholder: 'Celebrating with loved ones' }
	];

	let selectedCategory = $state('All');

	let filteredPhotos = $derived(selectedCategory === 'All' 
		? photos 
		: photos.filter(photo => photo.category === selectedCategory));

	function selectCategory(category: string) {
		selectedCategory = category;
	}
</script>

<svelte:head>
	<title>Photos - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Our Photos
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			A collection of our favorite moments together, from everyday adventures to special milestones.
		</p>
	</div>
</section>

<!-- Filter Section -->
<section class="bg-gray-50 py-12">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex flex-wrap justify-center gap-4">
			{#each photoCategories as category}
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

<!-- Photo Gallery -->
<section class="bg-gray-50 pb-20">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
			{#each filteredPhotos as photo}
				<div class="bg-white rounded-lg overflow-hidden shadow-sm hover:shadow-md transition-shadow duration-200">
					<div class="aspect-square bg-gray-100 flex items-center justify-center">
						<div class="text-center p-6">
							<svg class="w-12 h-12 text-gray-400 mx-auto mb-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
							</svg>
							<p class="text-sm text-gray-500 text-center">{photo.placeholder}</p>
						</div>
					</div>
					<div class="p-4">
						<h3 class="text-lg font-light text-black mb-1">{photo.title}</h3>
						<p class="text-sm text-gray-500">{photo.category}</p>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Coming Soon Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">More Photos Coming Soon</h2>
		<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
			We're constantly creating new memories together. Check back often to see the latest additions to our photo collection, including professional engagement photos and behind-the-scenes wedding planning moments.
		</p>
		<div class="bg-gray-50 p-8 rounded-lg">
			<p class="text-gray-600 mb-4">Want to share a photo with us?</p>
			<p class="text-sm text-gray-500">Email us at <span class="text-black">photos@gabrielandelyse.com</span></p>
		</div>
	</div>
</section>
