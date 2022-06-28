<script>
    export let BackgroudColor = "white";
    export let Show = false;
    export let from = "Bottom";
    export let zindex = "auto";

    let positionX = "0%";
    let positionY = "0%";

    let position = "0%";

    $:if(Show) {
        position = "0%";
        SlidingType();
    } else {
        position = "100%"
        SlidingType();
    }

    function SlidingType() {
        switch(from) {
            case "Bottom":
                positionY = position;
            break;

            case "Left":
                positionX = "-" + position;
            break;

            case "Top":
                positionY = "-" + position;
            break;

            case "Right":
                positionX = position;
            break;
        
            default:
            break;
        }
    }

</script>

<style>
    section{
        position: fixed;
        height: 100vh;
        width: 100%;
        transition: 700ms;
        overflow: hidden;
    }
</style>

<section 
    style="
        background:{BackgroudColor};
        transform:translate({positionX},{positionY});
        background-size: cover;
        z-index: {zindex};
    "
>
    <slot></slot>
</section>

