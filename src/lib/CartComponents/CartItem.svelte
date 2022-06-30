<script>
    export let id;
    export let color;
    export let X;
    export let Y;
    export let Z;
    export let n;
    export let price;


    let traver;

    let srcTraver;
    let BG;

    switch(color){
        case 0:
            srcTraver = '/TraverTexure.jpg';
            traver = "Classico";
        break;

        case 1:
            srcTraver = '/Travertino-Navona.jpg';
            traver = "Navona";
        break;

        case 2:
            srcTraver = '/travertino-noce.jpg';
            traver = "Noce";
        break;

        case 3:
            srcTraver = '/TravertinoSilver.webp';
            traver = "Silver";
        break;

        case 4:
            srcTraver = '/TravertinoAlabastrino.webp';
            traver = "Alabastrino";
        break;
    }

    if(id%2 == 0){
        BG = "white";
    }else{
        BG = "white";
    }


    function virgola(x) {
    	var parts = x.toString().split(".");
    	parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    	return parts.join(".");
	}
</script>

<style lang="scss">

    .resizer{
        display: flex;
        justify-content: center;
    }


    .FlexColumn{
        flex-direction: column;
        display: flex;
        text-align: left;
    }


    .CartItem{
        max-width: 1200px;
        width: 100%;
        padding: 1rem;
        display: flex;
        align-items: center;
        font-size: 1.2rem;
        text-align: center;
        justify-content: space-evenly;
        align-content: center;
        flex-direction: row;
        color: var(--Traver5);

        h1{
            width: 10rem;
        }

        img
        {
            height: 7rem;
            width: 7rem;
            border-radius: 20px;
        }

    }
    
    span{
        display: flex;
        align-items: center;
    }

    h2{
        margin: 0;
        margin-left: 1rem;
    }


    @media only screen and (max-width: 1000px) {
    .CartItem{
        flex-direction: column;
    }

    img
        {
            margin-bottom: 1.3rem;
        }


    }


</style>


<div class="resizer" style="background-color: {BG};">
    <div class="CartItem">

        <h1>{traver}</h1>

        <img src={srcTraver} alt="travertino">

        <div class="FlexColumn">
            <span>Larghezza: <h2>{X}cm</h2></span>
            <span>Profondità: <h2>{Y}cm</h2></span>
            <span>Altezza: <h2>{Z}cm</h2></span> 
        </div>
        


        <span>Numero pezzi: <br> <h2>{n}</h2></span>
        <span>Prezzo: <br> <h2>{virgola(price.toFixed(2))}€</h2></span>
    </div> 
</div>

<hr style="opacity: 0.3;">

