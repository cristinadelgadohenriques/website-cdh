<script>
  import { PrismicImage, PrismicLink } from '@prismicio/svelte';
  /** @type {import("@prismicio/client").Content.BookSlice} */
  export let slice;
</script>

<div class="flex gap-5 w-full items-stretch">
  <div class="flex flex-col items-end ml-[70px] min-w-[100px] gap-3 mt-2 mb-10">
    <span class="font-bold">{slice.primary.year}</span>
    {#if slice.primary.cover}
      <PrismicLink field={slice.primary.url}>
        <PrismicImage class="min-w-[100px] max-w-[100px]" width={100} field={slice.primary.cover} />
      </PrismicLink>
    {/if}
  </div>
  <div class="bg-[#F4F4F4] w-1"></div>
  <div class="flex flex-col gap-2 mt-2 mb-10">
    <span class="font-bold text-black">{slice.primary.title}</span>
    {@html slice.primary.references.replace(/\n/g, '<br>')}
    <PrismicLink class="underline" field={slice.primary.url}>{slice.primary.url.url}</PrismicLink>
  </div>
</div>