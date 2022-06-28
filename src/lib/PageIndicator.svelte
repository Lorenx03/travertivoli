<script>
    export let page;

    let contrast;
    let width = 100;

    $:if(page == 2){
        contrast = "#40210F";
    }
    else{
        contrast = "#FFFFFF";
    }


    $:if(page == 3){
        width = 70;
    }
    else{
        width = 100;
    }
    
</script>

<style lang="scss">

    .Bottom{
        z-index: 9999;
        position: fixed;
        width: 100%;
        display: flex;
        bottom: 0;
        justify-content: space-between;

        .SidePageIndicator{
            height: 2.2rem;
            width: 7rem;
            display: flex;
            align-items: flex-end;
            justify-content: space-evenly;
            align-content: center;
            flex-wrap: nowrap;
            transition: 300ms;
            padding-bottom: 1rem;
            padding-top: 0.5rem;
            -webkit-border-top-right-radius: 30px;
            -moz-border-radius-topright: 30px;
            border-top-right-radius: 30px;
            
            .selectPage{
                width: 3px;
                height: 1rem;
                background-color: var(--ContrastColor);
                border-radius: 100px;
                transition: 700ms;
            }

            .selectedPage{
                height: 2rem;
            }
        }

        .ScrollFlag{
            color: white;
            border-right: 2px white solid;
            font-size: 2rem;
            margin-right: 2rem;
            transition: 700ms;
            
            .scorriSpan{
                margin-right: 1rem;
                font-weight: 200;
            }
        }
    }

    .trasparent{
        transform: translateY(5rem);
    }
</style>

<div class="Bottom" style="width: {width}%;">
    <div class="SidePageIndicator" style="--ContrastColor:{contrast};">
        <div class="selectPage" class:selectedPage="{page == 0}"></div>
        <div class="selectPage" class:selectedPage="{page == 1}"></div>
        <div class="selectPage" class:selectedPage="{page == 2}"></div>
        <div class="selectPage" class:selectedPage="{page == 3}"></div>
    </div>

    <div class="ScrollFlag" class:trasparent="{page != 0}">
        <div style="transform: translateY(-0.6rem);">
           <span class="scorriSpan">Scorri</span>
        </div>  
    </div>
</div>