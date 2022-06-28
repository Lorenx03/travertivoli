<script>

    import { onMount } from 'svelte';
    var SlidingOffset = [0,0,0,0,0];

    onMount(()=> {
        setTimeout(() => {
            for (let i = 0; i < SlidingOffset.length; i++) {
                setTimeout(() => {
                    SlidingOffset[i] = 100;
                    
                }, (200*i));
            }
        }, 1200);
    });

    
</script>

<style lang="scss">
    .container { 
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-columns: 1.3fr 1fr;
        grid-template-rows: 1fr 1fr;
        gap: 0px 0px;
        grid-auto-flow: row;
        grid-template-areas:
        "text img"
        "img2 text2";

        .img { 
        grid-area: img;
        background-image: url("/TraverWork.webp");
        background-position: center;
        }

        .img2 { 
            grid-area: img2;
            background-image: url("/lavorazione-travertino-seppia.webp");
            background-size: cover;
            background-position: center;
        }

        .text2 { 
            grid-area: text2;
            
        }

        .text { 
            grid-area: text;
        }
    }


    .textContainer{
        padding: 3rem 4rem;
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        align-content: center;
        justify-content: center;

        h1{
            font-size: 3rem;
            margin: 0;
            color: var(--Traver5);
            transform: translateY(-1rem);
        }
        
        p{
            color: var(--Traver4);
            margin: 0;
            transform: translateY(-1rem);
            text-align: justify;
        }
    }

    .ColorBlockContainer{
        position: relative;
        height: 100%;
        width: 100%;

        .ColorBlock{
            position: absolute;
            height: 100%;
            width: 100%;
            transition: 1000ms;
        }
    }


    

    //Phone
    @media only screen and (max-width: 1000px) {
        
        .container { 
            width: 100%;
            height: 100%;
            display: grid; 
            grid-auto-columns: 1fr; 
            grid-template-columns: 100%; 
            grid-template-rows: 1fr 15% 1fr; 
            gap: 0px 0px; 
            grid-template-areas: 
                "text"
                "img"
                "text2"; 
        }

        .textContainer{
            padding: 1rem 4rem;
            display: flex;
            flex-direction: column;
            flex-wrap: nowrap;
            align-content: center;
            justify-content: center;

            h1{
                font-size: 3rem;
                margin: 0;
                color: var(--Traver5);
            }
            
            p{
                color: var(--Traver4);
                margin: 0;
                text-align: justify;
            }
        }

        .Qualitafix{
            transform: translateY(-4rem);
        }
    }


</style>




<div class="container">
  <div class="img">
    <div class="ColorBlockContainer">
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver5);
            transform: translateX({SlidingOffset[0]}%);
            z-index:6">
        </div>

        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver4);
            transform: translateX({SlidingOffset[1]}%);
            z-index:5">
        </div>
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver3);
            transform: translateX({SlidingOffset[2]}%);
            z-index:4">
        </div>
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver2);
            transform: translateX({SlidingOffset[3]}%);
            z-index:3">
        </div>
    </div>
  </div>

  <div class="img2">
    <div class="ColorBlockContainer">
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver5);
            transform: translateX(-{SlidingOffset[0]}%);
            z-index:6">
        </div>

        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver4);
            transform: translateX(-{SlidingOffset[1]}%);
            z-index:5">
        </div>
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver3);
            transform: translateX(-{SlidingOffset[2]}%);
            z-index:4">
        </div>
        <div 
            class="ColorBlock" 
            style="background-color:var(--Traver2);
            transform: translateX(-{SlidingOffset[3]}%);
            z-index:3">
        </div>
    </div>
  </div>

  <div class="text2 textContainer Qualitafix">
    <h1>Qualità</h1>
    <p>
        Il nostro travertino tiburtino è lavorato secondo gli standard industriali più alti, utilizzando macchine a controllo numerico di ultima generazione per garantire una finitura e qualità generale del prodotto senza paragoni.
        <br><br>
        tutto ciò è realizzato dai migliori macchinisti nel settore per garantire qualità ed affidabilità. Tutti i nostri prodotti vengono realizzati secondo le necessità del cliente, il quale viene assistito in tutto l'itere da un consulente specializzato.
    </p>
  </div>

  <div class="text textContainer">
    <h1>travertino</h1>
    <p>Il travertino è una pietra naturale incredibilmente resistente e compatta, molto utilizzata in edilizia. In particolare, il travertino è una roccia sedimentaria costituita soprattutto da minerali di carbonato di calcio.
        <br>
        <br>
    Il termine travertino deriva da “tiburtinus” poiché proveniente in larga misura da un’area sotto Tivoli. Il travertino, infatti, fu uno dei materiali più utilizzati dai romani per la costruzione di edifici e opere pubbliche tanto da essere poi diventato famoso proprio con l’appellativo travertino romano.
    <br><br>
    Il suo aspetto può variare dal color bianco al paglierino al noce, con cromature scure o chiare. Le tonalità a livello chimico, sono determinate dalla presenza o meno di molteplici ossidi naturali di origine vegetale, animale o mineraria.
    </p>
  </div>
</div>
