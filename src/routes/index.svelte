<script context="module">
</script>

<script>
    //import Hamburger from "$lib/hamburger.svelte";
    
    import Block from "$lib/block.svelte";
    import PeaksTransition from "$lib/Peaks/PeaksTransition.svelte";


    import IndexTitle from "$lib/ContentComponents/IndexTitle.svelte";
    import ChiSiamo from "$lib/ContentComponents/SecondPage.svelte";
    import PageIndicator from "$lib/PageIndicator.svelte";
    import LoadingAnim from "$lib/LoadingAnim.svelte";
    import ThirdPage from "$lib/ContentComponents/ThirdPageGrid.svelte";
    import FourthPage from "$lib/ContentComponents/FourthPage.svelte";
    
    let loaded = false;
    let LoadingScreenLife = true;
    setTimeout(() => {loaded = true},1000);
    setTimeout(() => {LoadingScreenLife = false},4000);
    
    let content = [IndexTitle, ChiSiamo];

    let ShowPage = [
        true,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false,
        false
    ];

    let page = 0;
    let TransitionDone = true;





//Scroll Logic
    function scroll(e) {
        if(e.deltaY > 0 && TransitionDone){
            GoFoward();
        } 
        else if(TransitionDone){
            GoBackwards();
        }
    }





//Scroll Animation Selection
    function SwitchPage() {
        switch (page) {
            case 0:
                TransitionDone = false;
                ShowPage[0] = true;
                
                for (let i = 9; i > 0; i--) {
                    setTimeout(() => {
                        ShowPage[i] = false;
                        //console.log(i);
                    }, 450-(100+(50*(i-2))));
                }

                setTimeout(() => {
                    TransitionDone = true;
                    ShowPage[10] = false;
                }, 1000);
            break;

            case 1:
                ShowPage[15] = false;
                setTimeout(() => {ShowPage[14] = false;},250);
                setTimeout(() => {ShowPage[13] = false;},450);
                setTimeout(() => {ShowPage[12] = false;},650);
                setTimeout(() => {ShowPage[11] = false;},1300);
                TransitionDone = false;

                ShowPage[1] = true;

                for (let i = 2; i < 10; i++) {
                    setTimeout(() => {
                        ShowPage[i] = true;
                        if(ShowPage[9] == true)
                            ShowPage[10] = true
                        //console.log(i);
                    }, 100+(50*(i-2)));
                }

                setTimeout(() => {
                    TransitionDone = true;
                    ShowPage[0] = false;
                    //console.log(ShowPage);
                }, 1200);
            break;

            case 2:
                ShowPage[20] = false;
                setTimeout(() => {ShowPage[19] = false;},250);
                setTimeout(() => {ShowPage[18] = false;},450);
                setTimeout(() => {ShowPage[17] = false;},650);
                setTimeout(() => {ShowPage[16] = false;},1300);
                TransitionDone = false;
                for (let i = 11; i <= 15; i++) {
                    setTimeout(() => {
                        ShowPage[i] = true;
                        //console.log(i);
                    },(200*(i-11)));
                }

                setTimeout(() => {
                    TransitionDone = true;
                    //console.log(ShowPage);
                }, 1200);
            break;

            case 3:
                TransitionDone = false;
                for (let i = 16; i <= 20; i++) {
                    setTimeout(() => {
                        ShowPage[i] = true;
                        //console.log(i);
                    },(200*(i-16)));
                }

                setTimeout(() => {
                    TransitionDone = true;
                    //console.log(ShowPage);
                }, 1200);
            break;
        
            default:
            break;
        }
    }





//Animate scrolling  
    function GoFoward() {
        if(TransitionDone && page < 3){
            page++;
            SwitchPage();
        }
        //console.log("foward");
    }

    function GoBackwards() {
        if(TransitionDone && page > 0){
            page--;
            SwitchPage();
        }
        //console.log("Backward");
    }






//Touch logic for scrolling
    let Touch = {
        InitialY: 0,
        FinalY:0
    };


    function TouchStart(e) {
        Touch.InitialY = e.changedTouches[0].screenY;
    }


    function TouchEnd(e) {
        Touch.FinalY = e.changedTouches[0].screenY;

        //console.log(Touch.InitialY, Touch.FinalY);

        if(Touch.InitialY - Touch.FinalY > 100)
            GoFoward();
        else if(Touch.InitialY - Touch.FinalY < -100)
            GoBackwards();
    }






//Detect Mobile
    

    let DeviceWidth = 1920;
    let Mobile = false;

    $:if(DeviceWidth < 1000)
        Mobile = true;
    else
        Mobile = false;


</script>








<svelte:head>
    <title>TraverTivoli</title>
    <link rel="preload" as="image" href="/Index-BG.jpg"/>

    <link rel="preload" as="image" href="/TraverWork.webp"/>

    <link rel="preload" as="image" href="/lavorazione-travertino-seppia.webp"/>

    <link rel="preload" as="document" href="https://maps.google.com/maps?q=41.95208629485354,%2012.75097727097055&t=k&z=15&ie=UTF8&iwloc=&output=embed"/>

    
    <link rel="icon" type="image/svg" href="/favicon.png" />

</svelte:head>



<svelte:body on:mousewheel|passive={scroll} on:touchstart|passive={TouchStart} on:touchend|passive={TouchEnd} />

<svelte:window bind:outerWidth={DeviceWidth} />

{#if LoadingScreenLife}
   <LoadingAnim visible={loaded} /> 
{/if}


<PageIndicator page={page}/>

<Block Show={ShowPage[0]} from={"Bottom"}>
    {#if ShowPage[0]}
        <svelte:component this={content[0]}/>
    {/if}
</Block>

{#if ShowPage[0]}
    <PeaksTransition ShowPage={ShowPage} MobileOpt={Mobile} />
{/if}
    

<Block BackgroudColor='white' Show={ShowPage[9]} from={"Bottom"}>
    {#if ShowPage[10]}
        <svelte:component this={content[1]}/>
    {/if}
</Block>


{#if ShowPage[11]}
    <Block BackgroudColor='#40210F' Show={ShowPage[12]} from={"Bottom"} />
    <Block BackgroudColor='#8C6B4F' Show={ShowPage[13]} from={"Right"} />
    <Block BackgroudColor='#BFA38A' Show={ShowPage[14]} from={"Left"} />

    <Block BackgroudColor='white' Show={ShowPage[15]} from={"Bottom"} >
        <ThirdPage />
    </Block>
{/if}



{#if ShowPage[16]}
    <Block BackgroudColor='#40210F' Show={ShowPage[17]} from={"Bottom"} />
    <Block BackgroudColor='#8C6B4F' Show={ShowPage[18]} from={"Left"} />
    <Block BackgroudColor='#BFA38A' Show={ShowPage[19]} from={"Top"} />

    <Block BackgroudColor='white' Show={ShowPage[20]} from={"Bottom"} >
        <FourthPage/>
    </Block>
{/if}


    




