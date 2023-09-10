<script>
	import Tab from '$lib/Tab.svelte';
	import { PrismicImage } from '@prismicio/svelte';
	import { createClient } from '$lib/prismicio';

	let gallery;
	const client = createClient();
	client.getSingle('gallery').then(data => gallery = data.data);

	const rowHeight = 200;
</script>

{#if gallery}
	<Tab>
		<div class="flex flex-wrap gap-2">
			{#each gallery.images as { image }}
				<a href={image.url} class="relative" style:width="{image.dimensions.width * rowHeight / image.dimensions.height}px" style:flex-grow={image.dimensions.width * rowHeight / image.dimensions.height} target="_blank" rel="noopener noreferrer">
					<i class="block" style:padding-bottom="{image.dimensions.height / image.dimensions.width * 100}%"></i>
					<PrismicImage class="absolute top-0 w-full align-bottom" width={image.dimensions.width} height={image.dimensions.height} field={image} />
				</a>
			{/each}
		</div>
	</Tab>
{/if}