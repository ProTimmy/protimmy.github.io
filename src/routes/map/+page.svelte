<script lang="ts">
	const mapSrc = "/map/edited_farm_map.png";
</script>

<svelte:head>
	<title>Map - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white pb-20">
	<div class="w-full bg-cover bg-center py-24 mb-12" style="background-image: linear-gradient(rgba(0,0,0,0.35), rgba(0,0,0,0.35)), url('/map/background.png');">
		<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
			<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-white tracking-wider mb-6">
				Map
			</h1>
			<div class="w-24 h-px bg-white mx-auto mb-8"></div>
			<p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto">
				A guide to Chimney Pond Farm & Lodge, where we'll be spending the whole weekend together.
			</p>
		</div>
	</div>
</section>

<!-- Map Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="text-center mb-10">
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Chimney Pond Farm & Lodge</h2>
			<div class="w-16 h-px bg-black mx-auto mb-6"></div>
			<p class="text-gray-600 max-w-2xl mx-auto">
				Every gathering on our <a href="/timeline" class="text-black underline underline-offset-2 hover:text-gray-600">Timeline</a> happens somewhere on this property — the Hilltop House, Lake House, Mountain House, Ridge Line House, the Ceremony Site, and more. Use this map to find your way around.
			</p>
		</div>

		<a
			href={mapSrc}
			target="_blank"
			rel="noopener noreferrer"
			class="block bg-white p-3 sm:p-4 rounded-lg shadow-sm hover:shadow-md transition-shadow duration-200"
		>
			<img
				src={mapSrc}
				alt="Illustrated map of Chimney Pond Farm & Lodge in Lake Glenville, NC, showing the Farmhouse & Bungalow, Hilltop House, Bridal Cabin, Ridge Line House, The Cabin, Overlook Porch, Ceremony Site, Groom's Cottage, Reception Venue & Hall, Free Standing Chimney, Chimney Pond, Mountain House, The Lake House, and Lake Glenville."
				class="w-full h-auto rounded"
				loading="lazy"
			/>
		</a>

		<p class="text-center text-sm text-gray-500 mt-4">
			Tap the map to open it full size.
		</p>
	</div>
</section>
