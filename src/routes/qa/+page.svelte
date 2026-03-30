<script lang="ts">
	const cpf = '/faq/cpf.jpg';
	const outfits_mens1 = '/faq/outfits-mens-1.jpeg';
	const outfits_mens2 = '/faq/outfits-mens-2.jpeg';
	const outfits_womens1 = '/faq/outfits-womens-1.jpeg';
	const outfits_womens2 = '/faq/outfits-womens-2.jpeg';

	interface FAQ {
		question: string;
		answer: string;
		isOpen: boolean;
		photos?: string[];
	}

	let faqs: FAQ[] = $state([
		{
			question: "Where is the wedding taking place?",
			answer: "We're getting married in the beautiful mountains of Cashiers, North Carolina. The venue is Chimney Pond Farms, a pine tree farm located in the heart of the Blue Ridge Mountains. For more information, please visit <a href='https://chimneypondfarm.com/'>their website</a>.",
			isOpen: false,
			photos: [cpf],
		},
		{
			question: "What should I wear?",
			answer: "Wear whatever makes you most comfortable!\n\n Our wedding ceremony will be in a grassy area, so we recommend flat shoes or wide heels. The weather may be warm, so lightweight fabrics may be more comfortable. Here are a couple of sample outfits that would look great with our wedding colors.", 
			isOpen: false,
			photos: [outfits_mens1, outfits_mens2, outfits_womens1, outfits_womens2],
		},
		{
			question: "Will the ceremony be indoors or outdoors?",
			answer: "We're planning an outdoor ceremony with an covered backup plan in case of weather. The reception will be held indoors with beautiful mountain views.",
			isOpen: false
		},
		{
			question: "When should I RSVP?",
			answer: "Please RSVP by May 1, 2026. You can respond online through this link or by mail using the card included with your invitation.",
			isOpen: false
		},
		{
			question: "Can I bring a plus-one?",
			answer: "Due to venue capacity, we're only able to accommodate guests specifically named on the invitation. If you have any questions about your invitation, please don't hesitate to reach out to us.",
			isOpen: false
		},
		{
			question: "Will there be an open bar?",
			answer: "Yes! We'll have a full open bar featuring beer, wine, and his & hers signature cocktails. We'll also have non-alcoholic options available.",
			isOpen: false
		},
		{
			question: "What about dietary restrictions?",
			answer: "We want to make sure everyone can enjoy the meal! Please let us know about any dietary restrictions or allergies when you RSVP, and we'll work with our caterer to accommodate your needs. Vegan & non-dairy entrée options will be available upon request.",
			isOpen: false
		},
		{
			question: "Is there parking available?",
			answer: "Yes, there will be complimentary parking available at the venue. There will also be a shuttle service from the parking lot to the ceremony site (10-15 min walk) and from the ceremony site to the reception (10 min walk through the pine trees).",
			isOpen: false
		},
		{
			question: "What time should I arrive?",
			answer: "To be determined! We are working with our wedding planner to determine the day-of timeline. Tentatively, we intend for the ceremony to be in the afternoon around 4pm.",
			isOpen: false
		},
		{
			question: "Are children welcome?",
			answer: "Yes! We are excited to celebrate with all of our loved ones regardless of age. Party headcount will include children and will be specified on your formal invitation. Please note that this is a lakefront, outdoor celebration and that it will be each guest's responsibility to watch for their children (child leashes not provided). We leave it up to parent's discretion whether they would like their child to attend.",
			isOpen: false
		},
		{
			question: "Will you have a wedding registry?",
			answer: "Yes! We will have some items listed in the <a href='https://withjoy.com/gabriel-and-elyse/registry'>wedding registry page</a>. We plan to continue living in our NY apartment and have collected everything we need for our daily lives. At this phase of our lives, we are most excited about new experiences. Wedding registry items may take the form of recommending new experiences, contributing to our honeymoon celebration, or our homeowner fund to support what comes next. Nonetheless, your presence is the greatest gift, and we are so excited to celebrate with you all.",
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

	function formatAnswer(answer: string): string {
		// Convert newlines to <br> tags for HTML rendering
		return answer.replace(/\n/g, '<br>');
	}
</script>

<style>
	:global(.faq-answer a) {
		color: #2563eb;
		text-decoration: underline;
		transition: color 0.2s;
	}

	:global(.faq-answer a:hover) {
		color: #1d4ed8;
	}
</style>

<svelte:head>
	<title>Q + A - Gabriel & Elyse Timotei</title>
</svelte:head>

<!-- Hero Section -->
<section class="bg-white pb-20">
	<div
		class="w-full bg-cover bg-center py-24 mb-12"
		style="background-image: linear-gradient(rgba(0,0,0,0.35), rgba(0,0,0,0.35)), url('/faq/cpf.png');"
	>
		<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
			<h1 class="text-4xl sm:text-5xl lg:text-6xl font-light text-white tracking-wider mb-6">
				Q + A
			</h1>
			<div class="w-24 h-px bg-white mx-auto mb-8"></div>
			<p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto">
				Everything you need to know about our special day. Can't find what you're looking for? Don't hesitate to reach out!
			</p>
		</div>
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
						class="w-full px-6 py-4 text-left flex items-center justify-between hover:bg-gray-50 transition-colors duration-200 cursor-pointer"
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
							{#if faq.photos && faq.photos.length > 0}
								<div class="flex gap-2 mb-4 overflow-x-auto overflow-y-hidden pb-2 -mx-6 px-6 {faq.photos.length === 1 ? 'justify-center' : ''}">
									{#each faq.photos as photo}
										<img src={photo} alt="" class="flex-shrink-0 w-auto h-100 rounded-lg object-contain"/>
									{/each}
								</div>
							{/if}
							<div class="faq-answer text-gray-600 leading-relaxed">{@html formatAnswer(faq.answer)}</div>
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
				<a href='mailto:info@timotei.wedding' class="text-black">info@timotei.wedding</a>
				<p class="text-sm text-gray-500 mt-4">We'll get back to you as soon as possible!</p>
			</div>
		</div>
	</div>
</section>
