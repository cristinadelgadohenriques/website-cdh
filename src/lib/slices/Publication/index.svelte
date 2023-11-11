<script>
  import { PrismicImage, PrismicLink, PrismicRichText } from '@prismicio/svelte';
  /** @type {import("@prismicio/client").Content.BookSlice} */
  export let slice, innerWidth;
</script>

<svelte:window bind:innerWidth />

<div class="flex gap-3 lg:gap-5 w-full items-stretch">
  <div class="flex flex-col items-end lg:ml-[70px] min-w-[70px] lg:min-w-[100px] gap-3 mt-2 mb-10">
    <span class="font-bold">{slice.primary.year}</span>
    {#if slice.primary.cover}
      <PrismicLink field={slice.primary.url}>
        <PrismicImage class="min-w-[70px] max-w-[70px] lg:min-w-[100px] lg:max-w-[100px]" width={innerWidth > 1024 ? 100 : 70} field={slice.primary.cover} />
      </PrismicLink>
    {/if}
  </div>
  <div class="bg-[#F4F4F4] min-w-[3px]"></div>
  <div class="flex flex-col gap-2 mt-2 mb-10 text-sm lg:text-md">
    <PrismicRichText field={slice.primary.title} />
    {slice.primary.isbn13 ? 'ISBN13: ' + slice.primary.isbn13 : ''}
    {slice.primary.isbn13 && slice.primary.isbn10 ? ' | ' : ''}
    {slice.primary.isbn10 ? 'ISBN10: ' + slice.primary.isbn10 : ''}
    {#if slice.primary.doi}
      <div>
        DOI: <a target="_blank" rel="noopener noreferrer" class="underline break-all" href={`https://doi.org/${slice.primary.doi}`}>{slice.primary.doi}</a>
      </div>
    {/if}
    {#if slice.primary.url.url}
      <div>
        <PrismicLink class="underline break-all" field={slice.primary.url}>{slice.primary.url.url}</PrismicLink>
      </div>
    {/if}
  </div>
</div>