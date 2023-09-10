<script>
	import Section from '$lib/Section.svelte';
	import Tab from '$lib/Tab.svelte';
	import { PrismicRichText } from '@prismicio/svelte';
	import { createClient } from '$lib/prismicio';

	let home;
	const client = createClient();
	client.getSingle('home').then(data => home = data.data);
</script>

{#if home}
	<Tab>
		<Section title="Short Biography">
			<PrismicRichText field={home.short_biography} />
		</Section>

		<a href={home.curriculum.url} class="flex items-center group text-[#5C5C5C] hover:text-[#333] transition-all font-bold gap-2" target="_blank" rel="noopener noreferrer">
			<span class="material-symbols-rounded">clinical_notes</span>
			<span class="group-hover:underline">Curriculum</span>
		</a>
	</Tab>
{/if}