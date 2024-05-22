<script>
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import { PrismicText, PrismicImage, SliceZone } from '@prismicio/svelte';

	import { components } from '$lib/slices';
	import Bounded from '$lib/components/Bounded.svelte';
	import TriangleGrid from '$lib/components/TriangleGrid.svelte';

	export let data;

	onMount(() => {
		const prefersReducedMotion = window.matchMedia('prefers-reduced-motion: reduce').matches;

		if (prefersReducedMotion) {
			gsap.set('.logo-image', { opacity: 1 });
			return;
		}

		const tl = gsap.timeline({
			defaults: {
				ease: 'power2.inOut'
			}
		});

		tl.fromTo(
			'.logo-image',
			{ y: 100, opacity: 0, scale: 0.6 },
			{ y: 0, opacity: 1, scale: 1, duration: 1, delay: 0.5 }
		);
	});
</script>

<Bounded>
	<div class="relative grid w-full place-items-center text-center">
		<TriangleGrid />
		<h1 class="text-5xl font-medium md:text-7xl">
			<PrismicText field={data.page.data.company} />
			<span class="block text-lg text-yellow-500">Case Study</span>
		</h1>
		<p class="mb-4 mt-8 max-w-xl text-balance text-lg text-slate-300">
			<PrismicText field={data.page.data.description} />
		</p>
		<PrismicImage field={data.page.data.image} class="logo-image rounded-lg opacity-0" />
	</div>
	<div class="mx-auto mt-12 md:mt-16">
		<SliceZone slices={data.page.data.slices} {components} />
	</div>
</Bounded>
