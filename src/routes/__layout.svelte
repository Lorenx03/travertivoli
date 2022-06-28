<script context="module">
  /** @type {import('@sveltejs/kit').Load} */
  export const load = async ({ url }) => ({ props: { url } });
</script>


<script>
    import PageTransition from '$lib/PageTransition.svelte';
    import '../styles/global.scss'

    export let url;
</script>


<PageTransition {url}>
   <slot></slot>  
</PageTransition>
 
