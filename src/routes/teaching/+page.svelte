<script>
  import Tab from '$lib/Tab.svelte';
  import { PrismicRichText } from '@prismicio/svelte';
  import Section from '$lib/Section.svelte';
	import { createClient } from '$lib/prismicio';

  let teaching;
	const client = createClient();
	client.getSingle('teaching').then(data => teaching = data.data);
</script>

{#if teaching}
  <Tab>
    {#each teaching.section as { title, content }}
      <Section {title}>
        <div class="ml-4 lg:ml-10 text-[#333] break-words">
          <PrismicRichText field={content} />
        </div>
      </Section>
    {/each}
  </Tab>
{/if}