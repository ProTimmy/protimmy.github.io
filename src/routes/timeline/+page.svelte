<script lang="ts">
	interface Event {
		time: string;
		name: string;
		location: string;
		description?: string;
		link?: { label: string; href: string };
		note?: string;
	}

	// A timeline item is a single event, a "choose one" pair, or a featured highlight.
	type TimelineItem = Event | { choose: Event[] } | { feature: Event };

	interface Day {
		weekday: string;
		date: string;
		summary: string;
		events: TimelineItem[];
	}

	const days: Day[] = [
		{
			weekday: "Friday",
			date: "July 31",
			summary: "A relaxed, optional day of gathering, with brunch, afternoon adventures, and a welcome dinner. We'd love for you to join, but we completely understand that not everyone can make it — no pressure at all.",
			events: [
				{
					time: "10 AM",
					name: "Rehearsal Brunch",
					location: "City Lights Cafe, Sylva NC",
					description: "Start the day together with a relaxed brunch in downtown Sylva."
				},
				{
					choose: [
						{
							time: "2 - 4 PM",
							name: "Bridal Party",
							location: "Hilltop House, on-site",
							description: "Time with the bride. All those staying on-site are welcome to join. Please direct any questions to Analise, the Maid of Honor."
						},
						{
							time: "2 - 4 PM",
							name: "Groom's Nature Walk",
							location: "Mountain House, on-site",
							description: "Meet at the Mountain House, where we'll head out together to the trail. The hike is a 2.2-mile loop starting at the Panthertown Valley Trailhead. All those staying on-site are welcome to join.",
							link: {
								label: "View the trail on AllTrails",
								href: "https://www.alltrails.com/trail/us/north-carolina/deep-gap-and-wilderness-falls-loop-trail"
							}
						}
					]
				},
				{
					time: "6 PM",
					name: "Welcome Dinner",
					location: "Lake House, on-site",
					description: "Come together for dinner by the lake to kick off the weekend."
				}
			]
		},
		{
			weekday: "Saturday",
			date: "August 1",
			summary: "The big day! Arrive for the ceremony, then celebrate with us into the night.",
			events: [
				{
					time: "3:30 - 4 PM",
					name: "Arrive for the Wedding",
					location: "The ceremony site, on-site",
					description: "Please plan to arrive between 3:30 and 4:00 PM so we can begin on time. Find your seat, and get ready to celebrate with us!"
				},
				{
					feature: {
						time: "4 - 11 PM",
						name: "The Wedding",
						location: "Chimney Pond Farm",
						description: "Ceremony, dinner, drinks, and dancing — the heart of the whole weekend."
					}
				},
				{
					time: "11 PM",
					name: "After Party",
					location: "Ridgeline House, on-site",
					description: "Keep the celebration going with us late into the night.",
					note: "21+ only"
				}
			]
		},
		{
			weekday: "Sunday",
			date: "August 2",
			summary: "One more day together before we say goodbye — join us for as much as you'd like.",
			events: [
				{
					time: "10 AM - 12 PM",
					name: "Farewell Brunch",
					location: "Farmhouse, on-site",
					description: "Ease into the morning with a leisurely brunch."
				},
				{
					time: "2 - 6 PM",
					name: "Field Day Games",
					location: "The free-standing Chimney near the Lake House",
					description: "Friendly games and outdoor fun. We'll gather on the venue site at the free-standing chimney."
				},
				{
					time: "7 - 10 PM",
					name: "Farewell Dinner",
					location: "Hilltop House, on-site",
					description: "A casual dinner of leftovers to close out the weekend together."
				}
			]
		}
	];
</script>

<svelte:head>
	<title>Timeline - Gabriel & Elyse Timotei</title>
</svelte:head>

{#snippet eventCard(event: Event, stacked: boolean)}
	<div class="bg-white p-6 rounded-lg shadow-sm hover:shadow-md transition-shadow duration-200 h-full">
		<div class={stacked ? "" : "sm:flex sm:items-start sm:gap-6"}>
			<!-- Time -->
			<div class="flex items-center text-black font-medium mb-2 {stacked ? '' : 'sm:mb-0 sm:w-44 sm:flex-shrink-0'}">
				<svg class="w-4 h-4 mr-2 flex-shrink-0 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
				</svg>
				<span>{event.time}</span>
			</div>

			<!-- Details -->
			<div class="flex-1">
				<h3 class="text-xl font-light text-black mb-2">{event.name}</h3>

				<div class="flex items-start text-gray-600 text-sm mb-3">
					<svg class="w-4 h-4 mr-2 flex-shrink-0 mt-0.5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
					</svg>
					<span>{event.location}</span>
				</div>

				{#if event.description}
					<p class="text-gray-600 leading-relaxed">{event.description}</p>
				{/if}

				{#if event.link}
					<a
						href={event.link.href}
						target="_blank"
						rel="noopener noreferrer"
						class="mt-3 inline-flex items-center text-sm text-black hover:text-gray-600 underline underline-offset-2"
					>
						{event.link.label}
						<svg class="w-3.5 h-3.5 ml-1 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
						</svg>
					</a>
				{/if}

				{#if event.note}
					<p class="mt-3 inline-block text-xs text-gray-500 bg-gray-100 px-3 py-1 rounded">{event.note}</p>
				{/if}
			</div>
		</div>
	</div>
{/snippet}

<!-- Hero Section -->
<section class="bg-white pb-20">
	<div class="w-full bg-cover bg-center py-24 mb-12" style="background-image: linear-gradient(rgba(0,0,0,0.35), rgba(0,0,0,0.35)), url('/timeline/background.png');">
		<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
			<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-white tracking-wider mb-6">
				Timeline
			</h1>
			<div class="w-24 h-px bg-white mx-auto mb-8"></div>
			<p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto">
				From arrival to farewell, here's how our wedding weekend will unfold. We can't wait to celebrate with you.
			</p>
		</div>
	</div>
</section>

<!-- Timeline -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 space-y-16">
		{#each days as day}
			<div>
				<!-- Day Header -->
				<div class="mb-8">
					<div class="flex items-baseline gap-3 flex-wrap">
						<h2 class="text-3xl sm:text-4xl font-light text-black">{day.weekday}</h2>
						<span class="text-lg text-gray-500 font-light">{day.date}</span>
					</div>
					<div class="w-16 h-px bg-black mt-4 mb-4"></div>
					<p class="text-gray-600 max-w-2xl">{day.summary}</p>
				</div>

				<!-- Events -->
				<div class="space-y-4">
					{#each day.events as item}
						{#if 'feature' in item}
							<!-- Featured highlight -->
							<div
								class="relative overflow-hidden rounded-lg bg-cover bg-center px-6 py-16 text-center shadow-md"
								style="background-image: linear-gradient(rgba(0,0,0,0.55), rgba(0,0,0,0.55)), url('/timeline/wedding-arch.jpg');"
							>
								<h3
									class="text-5xl sm:text-6xl text-white mb-4"
									style="font-family: 'Dancing Script', cursive; font-weight: 600;"
								>
									{item.feature.name}
								</h3>
								<div class="w-16 h-px bg-white/40 mx-auto mb-6"></div>
								<p class="text-2xl font-light tracking-wide text-white mb-2">{item.feature.time}</p>
								<div class="flex items-center justify-center text-sm text-gray-400">
									<svg class="w-4 h-4 mr-2 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
									</svg>
									<span>{item.feature.location}</span>
								</div>
								{#if item.feature.description}
									<p class="mt-6 max-w-md mx-auto text-gray-300 leading-relaxed">{item.feature.description}</p>
								{/if}
							</div>
						{:else if 'choose' in item}
							<!-- Either / or pair -->
							<div>
								<div class="relative grid gap-4 sm:grid-cols-2 items-stretch">
									{#each item.choose as option}
										{@render eventCard(option, true)}
									{/each}
									<!-- "or" badge centered between the two options -->
									<div class="pointer-events-none absolute left-1/2 top-1/2 z-10 -translate-x-1/2 -translate-y-1/2">
										<span class="flex h-10 w-10 items-center justify-center rounded-full border border-gray-200 bg-white text-xs font-medium uppercase tracking-wide text-gray-500 shadow-sm">
											or
										</span>
									</div>
								</div>
							</div>
						{:else}
							{@render eventCard(item, false)}
						{/if}
					{/each}
				</div>
			</div>
		{/each}
	</div>
</section>

<!-- Closing Note -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Questions?</h2>
		<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
			Times and details are our best plan for the weekend and may shift slightly. If anything is unclear, we're always happy to help.
		</p>
		<div class="bg-gray-50 p-8 rounded-lg">
			<p class="text-gray-600 mb-4">We can't wait to celebrate with you!</p>
			<p class="text-sm text-gray-500">Reach out to us at <a href="mailto:info@timotei.wedding" class="text-black hover:underline">info@timotei.wedding</a></p>
		</div>
	</div>
</section>
