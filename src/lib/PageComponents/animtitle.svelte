<script>
    import {  fade, slide, scale } from 'svelte/transition';
    export let Title = "";

    let w;
</script>



<style lang="scss">
    h1{
        font-size: 10rem;
        margin-top: 6rem;
        margin-bottom: 0;
        text-align: center;
        position: fixed;
        font-weight: 700;
        user-select: none;
        line-height: 1;
    }

    .AnimTitle{
        width: 100%;
        margin-top: 6rem;
    }


    .WidthH1{
        color: black;
        opacity: 0;
        width: 100%;
        
    }

    .centerDiv{
        width: 100%;
        position: fixed;

        .text{
            margin: 17rem auto;
        }
    }

    //Phone
    @media only screen and (max-width: 503px) {
        .centerDiv{
            width: 100%;
            position: fixed;

            .text{
                margin: 28rem auto;
            }
        }
    }
</style>



<h1 class="AnimTitle" in:scale="{{ duration: 2000}}" out:fade style="color: var(--Traver1);">{Title}</h1>

<h1 class="AnimTitle" in:slide="{{delay: 100, duration: 2000}}" out:fade style="color: var(--Traver2);" >{Title}</h1>

<h1 class="AnimTitle" in:slide="{{delay: 250, duration: 2000}}" out:fade style="color: var(--Traver3);">{Title}</h1>

<h1 class="AnimTitle" in:slide="{{delay: 400, duration: 2000}}" out:fade style="color: white">{Title}</h1>


<h1 class="WidthH1">
    <span bind:clientWidth={w} style="display: block; width:fit-content; margin: auto">{Title}</span>
</h1>


<div class="centerDiv">
    <div style="width: {w}px;" class="text">
        <slot />
    </div>
</div>


    
