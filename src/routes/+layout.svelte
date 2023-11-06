<script>
  import '../app.css';
  import { page } from '$app/stores';
	import { PrismicImage, PrismicLink } from '@prismicio/svelte';
  import { createClient } from '$lib/prismicio';
  $: currentTab = $page.route.id?.split('/')[1] || 'home';

  let header, footer, innerWidth, innerHeight;
	const client = createClient();
	client.getSingle('header').then(data => header = data.data);
	client.getSingle('footer').then(data => footer = data.data);

  const tabs = ['home', 'research', 'teaching', 'gallery'];
</script>

<svelte:window bind:innerWidth bind:innerHeight />

{#if header && footer}
  <div class="min-h-screen overflow-x-hidden flex flex-col items-center">
    <PrismicImage class="w-full h-36 lg:h-48 object-cover" height={innerWidth > 1024 ? 192 : 144} field={header.banner} />
    <PrismicImage class="rounded-full -translate-y-[70%] border-solid border-8 border-white h-36 lg:h-48 -mb-24 lg:-mb-28" height={innerWidth > 1024 ? 192 : 144} field={header.photo} />
    <h1 class="mx-5 font-serif font-bold text-3xl lg:text-4xl text-[#333] text-center">{header.name}</h1>
    <div class="my-8 lg:my-12 grow w-[90%] lg:w-[1000px] flex flex-col items-center">
      <div class="w-full relative flex border-b-[3px] border-[#F4F4F4] font-bold uppercase text-[#A5A5A5]">
        {#each tabs as tab}
          <a class="py-2 transition-all text-sm lg:text-base text-center {currentTab == tab ? 'text-[#333]' : ''}" style:width="{100 / tabs.length}%" href={tab.replace('home', '/')}>{tab}</a>
        {/each}
        <div class="absolute h-[3px] bg-[#333] -bottom-[3px] transition-all" style:width="{100 / tabs.length}%" style:left="{Math.max(tabs.indexOf(currentTab) * 100 / tabs.length, 0)}%"></div>
      </div>
      <div class="w-full mt-10">
        <slot />
      </div>
    </div>
    <div class="w-full p-4 bg-[#252525] flex justify-center items-center gap-4 lg:gap-24">
      <div class="flex flex-col justify-center gap-5 w-[200px] lg:w-[280px] opacity-75">
        {#each footer.logos as logo}
          <PrismicLink field={logo.url}>
            <PrismicImage class={logo.invert ? 'invert' : ''} field={logo.logo} />
          </PrismicLink>
        {/each}
      </div>
      <div class="text-[#909090] leading-snug text-xs lg:text-sm">
        <h2 class="text-[#BCBCBC] font-bold mb-1">Contact</h2>
        {@html footer.contact.replace(/\n/g, '<br>')}
      </div>
    </div>
  </div>
{/if}