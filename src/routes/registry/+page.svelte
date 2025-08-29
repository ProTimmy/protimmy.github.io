<script lang="ts">
	interface RegistryStore {
		name: string;
		description: string;
		website: string;
		registryId?: string;
		icon: string;
	}

	const registryStores: RegistryStore[] = [
		{
			name: 'Williams Sonoma',
			description:
				'Kitchen essentials, cookware, and entertaining pieces for our new home together.',
			website: 'williams-sonoma.com',
			registryId: 'gabriel-elyse-timotei',
			icon: '🍳'
		},
		{
			name: 'Crate & Barrel',
			description:
				'Modern furniture, home decor, and stylish housewares to make our space beautiful.',
			website: 'crateandbarrel.com',
			registryId: 'gabriel-elyse-wedding',
			icon: '🏠'
		},
		{
			name: 'REI Co-op',
			description: 'Outdoor gear and adventure equipment for all our hiking and camping trips.',
			website: 'rei.com',
			registryId: 'timotei-wedding',
			icon: '🏔️'
		},
		{
			name: 'Target',
			description: 'Everyday essentials, home goods, and practical items for our life together.',
			website: 'target.com',
			registryId: 'gabriel-elyse-2026',
			icon: '🎯'
		}
	];

	interface GiftIdea {
		category: string;
		items: string[];
	}

	const giftIdeas: GiftIdea[] = [
		{
			category: 'Kitchen & Dining',
			items: [
				'Stand mixer for our weekend baking adventures',
				'Cast iron Dutch oven for cozy dinners',
				'Quality knife set for cooking together',
				'Wine glasses for celebrating milestones',
				'Coffee maker for our morning routine'
			]
		},
		{
			category: 'Home & Living',
			items: [
				'Cozy throw blankets for movie nights',
				'Picture frames for our favorite memories',
				'Plants to brighten our home',
				'Candles for romantic dinners',
				'Board games for fun evenings in'
			]
		},
		{
			category: 'Adventure & Travel',
			items: [
				'Hiking backpacks for weekend adventures',
				'Camping gear for outdoor getaways',
				'Travel luggage for future trips',
				'Camera equipment to capture memories',
				'National Parks pass for exploring'
			]
		}
	];
</script>

<svelte:head>
	<title>Registry - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="mx-auto max-w-4xl px-4 text-center sm:px-6 lg:px-8">
		<h1 class="mb-6 text-4xl font-light tracking-wider text-black sm:text-5xl lg:text-6xl">
			Registry
		</h1>
		<div class="mx-auto mb-8 h-px w-24 bg-black"></div>
		<p class="mx-auto max-w-2xl text-lg text-gray-600 sm:text-xl">
			Your presence at our wedding is the greatest gift of all. If you'd like to honor us with a
			gift, we've registered at a few of our favorite places.
		</p>
	</div>
</section>

<!-- Registry Stores -->
<section class="bg-gray-50 py-20">
	<div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		<div class="mb-16 text-center">
			<h2 class="mb-4 text-3xl font-light text-black sm:text-4xl">Where We're Registered</h2>
			<div class="mx-auto h-px w-24 bg-black"></div>
		</div>

		<div class="grid gap-8 md:grid-cols-2">
			{#each registryStores as store}
				<div
					class="rounded-lg bg-white p-8 shadow-sm transition-shadow duration-200 hover:shadow-md"
				>
					<div class="mb-6 text-center">
						<div class="mb-4 text-4xl">{store.icon}</div>
						<h3 class="mb-2 text-2xl font-light text-black">{store.name}</h3>
						<p class="leading-relaxed text-gray-600">{store.description}</p>
					</div>

					<div class="space-y-3 text-center">
						{#if store.registryId}
							<p class="text-sm text-gray-500">
								Registry ID: <span class="text-black">{store.registryId}</span>
							</p>
						{/if}
						<div class="space-y-2">
							<button
								class="w-full bg-black px-6 py-3 font-light tracking-wide text-white transition-colors duration-200 hover:bg-gray-800"
							>
								View Registry
							</button>
							<p class="text-xs text-gray-500">{store.website}</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Gift Ideas -->
<section class="bg-white py-20">
	<div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		<div class="mb-16 text-center">
			<h2 class="mb-4 text-3xl font-light text-black sm:text-4xl">Gift Ideas</h2>
			<div class="mx-auto mb-6 h-px w-24 bg-black"></div>
			<p class="mx-auto max-w-2xl text-lg text-gray-600">
				Here are some things we're excited about as we start our married life together.
			</p>
		</div>

		<div class="grid gap-8 lg:grid-cols-3">
			{#each giftIdeas as category}
				<div class="rounded-lg bg-gray-50 p-6">
					<h3 class="mb-6 text-center text-xl font-light text-black">{category.category}</h3>
					<ul class="space-y-3">
						{#each category.items as item}
							<li class="flex items-start">
								<div class="mr-3 mt-2 h-2 w-2 flex-shrink-0 rounded-full bg-black"></div>
								<span class="text-sm text-gray-600">{item}</span>
							</li>
						{/each}
					</ul>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Honeymoon Fund -->
<section class="bg-gray-50 py-20">
	<div class="mx-auto max-w-4xl px-4 text-center sm:px-6 lg:px-8">
		<h2 class="mb-4 text-3xl font-light text-black sm:text-4xl">Honeymoon Fund</h2>
		<div class="mx-auto mb-8 h-px w-24 bg-black"></div>

		<div class="rounded-lg bg-white p-8">
			<div class="mb-6 text-6xl">✈️</div>
			<h3 class="mb-4 text-2xl font-light text-black">Safari Adventure in Kenya</h3>
			<p class="mb-6 leading-relaxed text-gray-600">
				We're planning an incredible honeymoon safari in Kenya to celebrate the start of our married
				life together. If you'd prefer to contribute to this once-in-a-lifetime adventure, we'd be
				so grateful!
			</p>

			<div class="space-y-4">
				<button
					class="inline-flex items-center bg-black px-8 py-3 font-light tracking-wide text-white transition-colors duration-200 hover:bg-gray-800"
				>
					Contribute to Honeymoon
				</button>
				<p class="text-sm text-gray-500">
					Contributions can be made through Zola or given as a check
				</p>
			</div>
		</div>
	</div>
</section>

<!-- Thank You Section -->
<section class="bg-white py-20">
	<div class="mx-auto max-w-4xl px-4 text-center sm:px-6 lg:px-8">
		<blockquote class="mb-8 text-2xl font-light italic text-black sm:text-3xl">
			"The best gifts are those that come from the heart, and your presence in our lives is the
			greatest gift of all."
		</blockquote>
		<p class="mb-8 text-lg text-gray-600">
			We're so grateful for your love and support as we begin this new chapter together. Whether you
			choose something from our registry or simply celebrate with us on our special day, your
			kindness means the world to us.
		</p>
		<div class="inline-block rounded-lg bg-gray-50 p-6">
			<p class="mb-2 text-gray-600">Questions about our registry?</p>
			<p class="text-sm text-gray-500">
				Email us at <span class="text-black">registry@gabrielandelyse.com</span>
			</p>
		</div>
	</div>
</section>
