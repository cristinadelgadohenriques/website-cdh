<script>
  import { fade } from 'svelte/transition';
</script>

<div class="leading-7 text-[#5C5C5C] mb-20" in:fade={{ duration: 150, delay: 150 }} out:fade={{ duration: 150 }}>
  <slot />
</div>