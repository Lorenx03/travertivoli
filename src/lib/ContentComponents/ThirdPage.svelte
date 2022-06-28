<script>
    import { onMount } from 'svelte';
    import anime from "animejs";
    let svg;
    let poly;

    let initPath = "0 980,125 982,250 993,375 959,500 961,625 956,750 986,875 966,1000 992,1125 985,1250 986,1375 947,1500 940,1625 953,1750 973,1875 974,2000 940,2000 1081,1875 1081,1750 1081,1625 1081,1500 1081,1375 1081,1250 1081,1125 1081,1000 1081,875 1081,750 1081,625 1081,500 1081,375 1081,250 1081,125 1081,0 1081";

    let animePath = "0 972,125 971,250 949,375 993,500 976,625 971,750 981,875 960,1000 946,1125 953,1250 944,1375 985,1500 974,1625 971,1750 965,1875 952,2000 959,2000 1081,1875 1081,1750 1081,1625 1081,1500 1081,1375 1081,1250 1081,1125 1081,1000 1081,875 1081,750 1081,625 1081,500 1081,375 1081,250 1081,125 1081,0 1081";

    let color = "white";
    
    //https://www.youtube.com/watch?v=ePFw62HISRI

    onMount(()=> {
        anime({
            targets: [svg, poly],
            points: [
                { value:  animePath},
            ],
            loop:true,
            direction: 'alternate',
            easing: 'linear',
            duration: 3000
        });
    });        
</script>

<style lang="scss">
    .BG{
        height: 100%;
        width: 100%;
        background-image: url("/TraverWork.webp");
        position: absolute;
        top: 0;
        left: 0;
        background-position: right 25%;

        .content{
            display: flex;
            height: 100%;
            flex-direction: column;
            flex-wrap: nowrap;
            justify-content: space-between;
            align-items: flex-start;

            .title{
                color: white;
                flex: 40%;
                display: flex;
                align-items: center;
                justify-content: center;
                flex-direction: row;
                flex-wrap: nowrap;
                align-content: center;
                width: 100%;
                

                h1{
                    font-size: 11.1rem;
                    margin: 0;
                    transform: translateY(-1.5rem);
                }
            }

            
            

            .text{
                background-color: white;
                flex: 60%;
                display: flex;
                justify-content: flex-start;
                align-content: center;
                flex-direction: column;
                align-items: center;
                width: 100%;
                opacity: 1;
                
                .peaksContaner
                {
                    .peaks{
                        transform: translateY(-92%);
                    }
                    height: 1rem;
                }
                

                span{
                    padding: 2rem;
                    text-align: justify;
                    max-width: 1000px;
                    z-index: 999999;
                    font-size: 1.2rem;
                }
            }
        }
    }


    //Laptop
    @media only screen and (max-width: 1500px) {
        .BG{
            .content{
                .title{
                    flex: 30%;
                    h1{
                        font-size: 7.5rem;
                    }
                }

                .text{
                    flex: 70%;
                    span{
                        font-size: 1.6rem;
                    }
                }
            }
        }
    }

</style>

<div class="BG">
    
    <div class="content">
        <div class="title">
            <h1>Travertino</h1>
        </div>
        
        <div class="text">
            <div class="peaksContaner">
            <div class="peaks">
                <svg
                    bind:this={svg}
                    id="visual"
                    viewBox="0 0 2000 1080"
                    width="2000"
                    height="1080"
                    xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                    version="1.1"
                >
                    <polygon bind:this={poly}
                        style=""
                        stroke="none"
                        fill={color}
                        points={initPath}
                    />
                </svg>
            </div>
            </div>

            <span>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Accusamus dolores fugit ipsa nostrum perspiciatis! Ullam rem facere id corporis, sed delectus porro eum quod ipsum, voluptatibus rerum, soluta dolor. Beatae!</span>
        </div>

    </div>
</div>
