<script>
  import { PrismicImage, PrismicLink } from '@prismicio/svelte';
  /** @type {import("@prismicio/client").Content.ProjectSlice} */
  export let slice;
</script>

<div class="flex flex-col lg:flex-row gap-5 lg:gap-11 lg:items-center w-full my-10">
  <PrismicLink field={slice.primary.url}>
    <PrismicImage class="min-w-[170px] max-w-[170px]" width={170} field={slice.primary.logo} />
  </PrismicLink>
  <div class="flex flex-col gap-2">
    <PrismicLink class="font-bold text-black underline" field={slice.primary.url}>{slice.primary.title}</PrismicLink>
    {slice.primary.description}
  </div>
</div>