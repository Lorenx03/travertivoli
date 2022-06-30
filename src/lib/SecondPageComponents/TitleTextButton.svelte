<script>
    import Animtitle from '$lib/PageComponents/animtitle.svelte';

    import { onMount } from 'svelte';
    import anime from "animejs";

    let revealBox;
    let BorderOpacity = {
        Opacity: 1
    }

    let BorderOpacityNumber;
    

    onMount(()=> {
        anime({
            targets: revealBox,
            height: ['0px','400px'],
            easing: 'easeInOutQuad',
            delay:500,
            duration: 1500
        }); 

        anime({
            targets: BorderOpacity,
            Opacity:0,
            easing: 'easeInOutQuad',
            delay:500,
            duration: 1500,
            round: 100,
            update: function(){
                BorderOpacityNumber = BorderOpacity.Opacity;
            }
        }); 
    });
</script>

<style lang="scss">

    .revealBox{
        border-bottom: 3px solid rgba(255, 255, 255, 1);
        overflow: hidden;
        display: flex;
        flex-direction: column;
        align-items: center;
        

        p{
            font-size: 1.2rem;
            text-align: justify;
            line-height: 1.3;
            color: white;
            margin: 0;
        }

        b{
            font-size: 1.3rem;
        }


        a{
            width: 100%;
            display: flex;
            justify-content: center;
            text-decoration: none;
            
            button{
                display: block;
                margin: 2rem 0;
                width: 65%;
                padding: 0.7rem;
                font-size: 1.5rem;
                font-family: 'Poppins', sans-serif;
                border: 4px var(--Traver2) solid;
                background-color: var(--Traver1);
                color: var(--Traver5);
                transition: 700ms;
                cursor: pointer;
                letter-spacing: 2px;
                border-radius: 100px;
            }

            button:hover{
                background-color: var(--Traver1);
                border: 4px var(--Traver5) solid;
                color: var(--Traver5);
                transform: scale(1.1);
            }
        }
    }
    
    

    @media only screen and (max-width: 1200px) {
        .revealBox{
            p{
                font-size: 1.6rem;
            }

            b{
                font-size: 1.6rem;
            }

            button{
                display: block;
                margin: 3rem 0;
                width: 80%;
                padding: 1.2rem;
                font-size: 2rem;
                font-family: 'Poppins', sans-serif;
                border: 2px white solid;
                background-color: rgba(0, 0, 0, 0);
                color: white;
                transition: 700ms;
                cursor: pointer;
                letter-spacing: 2px;
                border-radius: 100px;
            }
        }
    }


    @media only screen and (max-width: 503px) {
        .revealBox{
            margin: 0rem 3rem;
        }
    }
    
</style>





    
<Animtitle Title="Chi siamo">

    <div class="revealBox" bind:this={revealBox} style="border-bottom:3px solid rgba(255, 255, 255, {BorderOpacityNumber});">
        <p>
        Siamo un’azienda che si occupa della creazione, lavorazione e consegna di pezzi in <b>travertino</b>, completamente personalizzabili.
        <br><br>
        Ci avvaliamo delle ultime <b>tecnologie</b> e processi industriali per offrire ai nostri clienti un prodotto di <b>qualità</b> e <b>duraturo</b>.
        <br><br>
        Premendo il bottone qua sotto potete accedere alla nostra <b>WebApp</b> per personalizzare il vostro travertino.
        </p>

        
        <a sveltekit:prefetch href="/editor"><button> Inizia a creare </button></a>
    </div>
    
</Animtitle>
