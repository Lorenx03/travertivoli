<script>
    import { onMount } from 'svelte';
    import anime from "animejs";
    let WindowWidth;
    let WindowHeight;

    let Triangles = [];

    onMount(()=> {
        anime({
            targets: Triangles,
            translateY: ['100%', '15%'],
            duration: 2000,
            easing: "easeOutBack"
        });  
    });

</script>

<style lang="scss">
    .BGfix{
        position: fixed;
        width: 100%;
        height: 40%;
        background-color: var(--Traver4);
    }

    .TriangleDeco{
        position: fixed;
        width: 100%;
        
        div{
            position: fixed;
            width: 0;
            height: 0;
            border-style: solid;
            border-width: 0 1920px 100px 0;
            border-color: transparent #007bff transparent transparent;
        }
    }
</style>



<svelte:window bind:innerWidth={WindowWidth} bind:innerHeight={WindowHeight}/>

<div class="BGfix"></div>


<div class="TriangleDeco">
    <div 
        bind:this={Triangles[4]}
        style="
        border-color:var(--Traver4) transparent transparent transparent;
        border-width:{WindowHeight*1.2}px {WindowWidth}px 0 0;
        z-index:0;
        Opacity: 0.6;
    "></div>

    <div
        bind:this={Triangles[3]}
        style="
        border-color: transparent var(--Traver4) transparent transparent;
        border-width: 0 {WindowWidth}px {WindowHeight}px 0;
        z-index:1;
    "></div>

    <div
        bind:this={Triangles[2]} 
        style="
        border-color:#75553f transparent transparent transparent;
        border-width:{WindowHeight*0.8}px {WindowWidth}px 0 0;
        z-index: 2;
    "></div>

    <div
        bind:this={Triangles[1]} 
        style="
        border-color: transparent var(--Traver3) transparent transparent;
        border-width: 0 {WindowWidth}px {WindowHeight*0.6}px 0;
        z-index: 3;
    "></div>

    <div
        bind:this={Triangles[0]} 
        style="
        border-color:var(--Traver4) transparent transparent transparent;
        border-width:{WindowHeight*0.4}px {WindowWidth}px 0 0;
        z-index: 4;
    "></div>

    <div 
        style="
        border-color: transparent var(--Traver5) transparent transparent;
        border-width: 0 {WindowWidth}px {WindowHeight*0.2}px 0;
        z-index: 5;
    "></div>
</div>