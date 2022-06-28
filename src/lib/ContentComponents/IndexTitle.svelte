<div class="TitleSection">

    <div class="WhiteBG">
        <h1>
            Traver
            <br />
            Tivoli
            <br />
            <span>Il lusso su misura</span>
        </h1>

        <img src="logo.svg" alt="logo" />
    </div>
</div>


<style lang="scss">
    @mixin FullH-FullW {
        width: 100%;
        height: 100%;
    }



    .TitleSection {
        @include FullH-FullW;

        background-image: url("/Index-BG.jpg");

        
        .WhiteBG {
            background-color: rgb(255, 255, 255);
            @include FullH-FullW;
            
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0;
            color: rgb(0, 0, 0);
            gap: 2rem;
            mix-blend-mode: screen;
            overflow: hidden;
            
            
            

            h1{
                line-height: 100%;
                text-align: left;
                user-select: none;
                font-size: 15rem;
                transform: translateY(2rem);
                

                span{
                    font-size: 2rem;
                    line-height: 1;
                    vertical-align: top;
                    margin-left:3.1rem;
                }
            }

            img{
                height: 50%;
                -webkit-user-drag: none;
                transform: translateY(-3rem);
            }
        }

    }


//Laptop
@media only screen and (max-width: 1500px) {
        .TitleSection {  
            .WhiteBG {
                img{
                    height: 40%;
                    -webkit-user-drag: none;
                }
            }
        }
    }    



//Phone
    @media only screen and (max-width: 800px) {
        .TitleSection {  
            .WhiteBG {
                flex-direction: column-reverse;

                h1{
                    margin-top: 0;
                    height: 25%;
                    transform: translateY(-7rem);
                    font-size: 11rem;
                    

                    span{
                        margin-left: 2.4rem;
                        font-size: 1.8rem;
                    }
                }

                img{
                    height: 30%;
                    transform: translateY(-7rem);
                }
            }
        }
    }
</style>