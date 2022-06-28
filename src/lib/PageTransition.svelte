<script>
  import { fade } from "svelte/transition";
  export let url = "";
  const pageTransitionDuration = 500;
</script>

{#key url}
  <div transition:fade>
    <slot />
  </div>
{/key}