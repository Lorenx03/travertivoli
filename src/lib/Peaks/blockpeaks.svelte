<script>
    import PeaksMorph from "./peaksMorph.svelte";

    export let BackgroudColor = "#bfa38a";
    export let Show = false;
    
    export let InitPathPeak = "0 980,125 982,250 993,375 959,500 961,625 956,750 986,875 966,1000 992,1125 985,1250 986,1375 947,1500 940,1625 953,1750 973,1875 974,2000 940,2000 1081,1875 1081,1750 1081,1625 1081,1500 1081,1375 1081,1250 1081,1125 1081,1000 1081,875 1081,750 1081,625 1081,500 1081,375 1081,250 1081,125 1081,0 1081";

    export let AnimPathPeak = "0 972,125 971,250 949,375 993,500 976,625 971,750 981,875 960,1000 946,1125 953,1250 944,1375 985,1500 974,1625 971,1750 965,1875 952,2000 959,2000 1081,1875 1081,1750 1081,1625 1081,1500 1081,1375 1081,1250 1081,1125 1081,1000 1081,875 1081,750 1081,625 1081,500 1081,375 1081,250 1081,125 1081,0 1081";

    let position = "100%";

    $:if (!Show) {
        position = "100%";
    } else {
        position = "0%"
    }

</script>

<style>
    section{
        position: fixed;
        height: 100vh;
        width: 100%;
        bottom: 0;
        transition: 700ms;
    }
    
    
</style>



<section 
    style="
        background-color:{BackgroudColor};
        transform:translateY({position})
    "
>
    <PeaksMorph 
        color="{BackgroudColor}"
        initPath="{InitPathPeak}"
        animePath="{AnimPathPeak}"
    />
</section>