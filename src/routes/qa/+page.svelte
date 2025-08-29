<script lang="ts">
	interface FAQ {
		question: string;
		answer: string;
		isOpen: boolean;
	}

	let faqs: FAQ[] = $state([
		{
			question: "When is the wedding?",
			answer: "Our wedding will take place on Friday, August 1, 2026. The ceremony begins at 5:00 PM, with the reception immediately following.",
			isOpen: false
		},
		{
			question: "Where is the wedding taking place?",
			answer: "We're getting married in the beautiful mountains of Cashiers, North Carolina. Detailed venue information and directions will be sent with your invitation.",
			isOpen: false
		},
		{
			question: "What should I wear?",
			answer: "We've chosen cocktail attire for our wedding. Think semi-formal dress - suits for men and cocktail dresses or dressy separates for women. Given the mountain location, comfortable shoes are recommended!",
			isOpen: false
		},
		{
			question: "Will the ceremony be indoors or outdoors?",
			answer: "We're planning an outdoor ceremony with an indoor backup plan in case of weather. The reception will be held indoors with beautiful mountain views.",
			isOpen: false
		},
		{
			question: "When should I RSVP?",
			answer: "Please RSVP by June 1, 2026. You can respond online through this website or by mail using the card included with your invitation.",
			isOpen: false
		},
		{
			question: "Can I bring a plus-one?",
			answer: "Due to venue capacity, we're only able to accommodate guests specifically named on the invitation. If you have any questions about your invitation, please don't hesitate to reach out to us.",
			isOpen: false
		},
		{
			question: "Will there be an open bar?",
			answer: "Yes! We'll have a full open bar featuring beer, wine, and signature cocktails. We'll also have non-alcoholic options available.",
			isOpen: false
		},
		{
			question: "What about dietary restrictions?",
			answer: "We want to make sure everyone can enjoy the meal! Please let us know about any dietary restrictions or allergies when you RSVP, and we'll work with our caterer to accommodate your needs.",
			isOpen: false
		},
		{
			question: "Is there parking available?",
			answer: "Yes, there will be complimentary parking available at the venue. We'll also have shuttle service from recommended hotels in the area.",
			isOpen: false
		},
		{
			question: "What time should I arrive?",
			answer: "Please plan to arrive by 4:45 PM so we can start the ceremony promptly at 5:00 PM. This will give you time to find parking and get seated.",
			isOpen: false
		},
		{
			question: "Are children welcome?",
			answer: "While we love children, we've decided to have an adults-only celebration to allow everyone to relax and enjoy the evening. We hope you understand and can arrange childcare for the night.",
			isOpen: false
		},
		{
			question: "Will you have a wedding registry?",
			answer: "Yes! We're registered at several stores, and you can find all the details on our Registry page. Your presence is the greatest gift, but if you'd like to give something, we'd be so grateful.",
			isOpen: false
		},
		{
			question: "Can I take photos during the ceremony?",
			answer: "We've hired a professional photographer to capture all the special moments. We kindly ask that you keep phones and cameras put away during the ceremony so everyone can be fully present. Feel free to take photos during the reception!",
			isOpen: false
		},
		{
			question: "What if I need to cancel last minute?",
			answer: "We understand that sometimes things come up. If you need to change your RSVP, please let us know as soon as possible so we can adjust our final headcount accordingly.",
			isOpen: false
		}
	]);

	function toggleFAQ(index: number) {
		faqs[index].isOpen = !faqs[index].isOpen;
	}
</script>

<svelte:head>
	<title>Q + A - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-black tracking-wider mb-6">
			Q + A
		</h1>
		<div class="w-24 h-px bg-black mx-auto mb-8"></div>
		<p class="text-lg sm:text-xl text-gray-600 max-w-2xl mx-auto">
			Everything you need to know about our special day. Can't find what you're looking for? Don't hesitate to reach out!
		</p>
	</div>
</section>

<!-- FAQ Section -->
<section class="bg-gray-50 py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="space-y-4">
			{#each faqs as faq, index}
				<div class="bg-white rounded-lg shadow-sm border border-gray-100 overflow-hidden">
					<button
						onclick={() => toggleFAQ(index)}
						class="w-full px-6 py-4 text-left flex items-center justify-between hover:bg-gray-50 transition-colors duration-200"
					>
						<h3 class="text-lg font-light text-black pr-4">{faq.question}</h3>
						<svg 
							class="w-5 h-5 text-gray-500 transform transition-transform duration-200 {faq.isOpen ? 'rotate-180' : ''}"
							fill="none" 
							stroke="currentColor" 
							viewBox="0 0 24 24"
						>
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
						</svg>
					</button>
					{#if faq.isOpen}
						<div class="px-6 pb-4">
							<p class="text-gray-600 leading-relaxed">{faq.answer}</p>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Contact Section -->
<section class="bg-white py-20">
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
		<h2 class="text-3xl sm:text-4xl font-light text-black mb-4">Still Have Questions?</h2>
		<p class="text-lg text-gray-600 mb-8 max-w-2xl mx-auto">
			We're here to help! If you have any other questions about our wedding day, don't hesitate to reach out to us directly.
		</p>
		<div class="bg-gray-50 p-8 rounded-lg">
			<p class="text-gray-600 mb-4">Get in touch with us:</p>
			<div class="space-y-2">
				<p class="text-black">Gabriel: <span class="text-gray-600">gabriel.timotei@email.com</span></p>
				<p class="text-black">Elyse: <span class="text-gray-600">elyse.timotei@email.com</span></p>
				<p class="text-sm text-gray-500 mt-4">We'll get back to you as soon as possible!</p>
			</div>
		</div>
	</div>
</section>
