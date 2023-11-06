<script>
  import Section from '$lib/Section.svelte';
  import Subsection from '$lib/Subsection.svelte';
  import Tab from '$lib/Tab.svelte';
	import { createClient } from '$lib/prismicio';

  import { SliceZone } from '@prismicio/svelte';
  import { components } from '$lib/slices';

  let projects, books, chapters, papers, databases;
	const client = createClient();
	client.getSingle('projects').then(data => projects = data.data);
  client.getSingle('books').then(data => books = data.data);
  client.getSingle('book_chapters').then(data => chapters = data.data);
  client.getSingle('papers').then(data => papers = data.data);
  client.getSingle('databases').then(data => databases = data.data);

  $: console.log(papers);
</script>

<Tab>
  <Section title="Research Projects">
    <SliceZone slices={projects?.slices} components={components} />
  </Section>
  <Section title="Publications">
    <Subsection title="Books">
      <SliceZone slices={books?.slices} components={components} />
    </Subsection>
    <Subsection title="Book Chapters">
      <SliceZone slices={chapters?.slices} components={components} />
    </Subsection>
    <Subsection title="Papers">
      <SliceZone slices={papers?.slices} components={components} />
    </Subsection>
    <Subsection title="Databases">
      <SliceZone slices={databases?.slices} components={components} />
    </Subsection>
  </Section>
</Tab>