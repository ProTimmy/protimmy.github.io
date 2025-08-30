<script lang="ts">
	// This page will be populated with wedding day photos after the event
	const weddingDate = "August 2026";
</script>

<svelte:head>
	<title>Photos - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Wedding Photos
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			Our wedding day memories will be shared here after {weddingDate}.
		</p>
	</div>
</section>

<!-- Coming Soon Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<div class="bg-white p-12 rounded-lg shadow-sm border border-gray-100">
			<svg class="w-24 h-24 text-gray-300 mx-auto mb-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z"></path>
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z"></path>
			</svg>
			<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Photos Coming Soon</h2>
			<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
				We can't wait to share the beautiful moments from our special day with you! Professional photos and candid shots from our wedding will be available here after the celebration.
			</p>
			<div class="space-y-4">
				<p class="text-gray-600">What to expect:</p>
				<div class="grid md:grid-cols-3 gap-4 text-sm text-gray-500">
					<div class="bg-gray-50 p-4 rounded">
						<strong class="text-black">Ceremony</strong><br>
						Capturing our vows and first moments as married couple
					</div>
					<div class="bg-gray-50 p-4 rounded">
						<strong class="text-black">Reception</strong><br>
						Dancing, toasts, and celebration with our loved ones
					</div>
					<div class="bg-gray-50 p-4 rounded">
						<strong class="text-black">Portraits</strong><br>
						Beautiful couple and family photos in the mountains
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Share Photos Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Share Your Photos</h2>
		<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
			Did you capture a special moment at our wedding? We'd love to see and share your photos with everyone!
		</p>
		<div class="bg-gray-50 p-8 rounded-lg">
			<p class="text-gray-600 mb-4">Send us your wedding photos</p>
			<p class="text-sm text-gray-500">Email: <span class="text-black">photos@gabrielandelyse.com</span></p>
			<p class="text-sm text-gray-500 mt-2">Or tag us on social media with <span class="text-black">#GabrielAndElyse2026</span></p>
		</div>
	</div>
</section>
