<script>
    let SuccessBannerPos = 100;
    let form;

    function SubmitForm(e){
        const data = new FormData(form);
        const action = e.target.action;
        fetch(action, {
        method: 'POST',
        body: data,
        })
        .then(() => {
            PostSuccess();
        })
    }


    function PostSuccess() {
        SuccessBannerPos = 0;
    }
</script>















<style lang="scss">
    @mixin formStyles{
        margin: 0.7rem;
        padding: 0.7rem;
        width: 100%;
        border-radius:30px;
        border: 2px var(--Traver5) solid;
        font-family: 'Poppins', sans-serif;
        color: var(--Traver5);
        background-color: white;
        text-align: center;
        transition: 700ms;
        font-size: 1rem;
    }

    @mixin FlexCenter{
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        align-content: center;
        justify-content: center;
        align-items: center;
    }


    ::placeholder{
        color: var(--Traver3);
    }









    .container {
        height: calc(100% - 4rem);
        width: 100%;
        display: grid; 
        grid-template-columns: 1fr 1fr 1fr; 
        grid-template-rows: 1fr; 
        gap: 0px 0px; 
        grid-template-areas: 
        "form map editor";








        .form {
            .SuccessBanner{
                position: absolute;
                background-color: var(--Traver4);
                height: 100%;
                width: 100%;
                transition: 700ms;
                @include FlexCenter;
                
                h2{
                    color: white;
                    font-size: 1.5rem;
                    text-align: center;
                }

            }




            padding: 2rem;
            grid-area: form;
            background-color: white;
            
            @include FlexCenter;

            h2{
                margin: 0;
                color: var(--Traver5);
                font-size: 3rem;
            }
            
            form{
                @include FlexCenter;

                input{
                    @include formStyles;
                }

                input:focus{
                   border-radius:10px;
                   min-width: 60%;
                }

                input:hover, textarea:hover {
                    background-color: var(--Traver5);
                    color: white;
                }

                textarea{
                    @include formStyles;
                    height: 3rem;
                    resize: none;
                }

                textarea:focus{
                    height: 8rem;
                    border-radius:10px;
                }

                #SubButt{
                    transition: 700ms;
                    cursor: pointer;
                    letter-spacing: 2px;
                    background-color: var(--Traver4);
                    color: white;
                    border: white;
                }

                #SubButt:hover{
                    transform: scale(1.1);
                }
            }
        }




        .map { grid-area: map; }




        .editor {
            grid-area: editor;
            background-image: url("/TraverWork.webp");

            .EditorContent{
                width: 100%;
                height: 100%;
                background-color: white;
                mix-blend-mode: screen;
                @include FlexCenter;

                img{
                    width: 65%;
                }

                h2{
                    text-align: center;
                    margin: 2.6rem;
                    font-weight: 900;
                    font-size: 1.7rem;
                }

                button{
                    width: 100%;
                    border: 4px solid black;
                    padding: 0.7rem 2rem;
                    font-size: 1.4rem;
                    font-family: 'Poppins', sans-serif;
                    background-color: white;
                    border-radius: 50px;
                    font-weight: 900;
                    transition: 700ms;
                    cursor: pointer;
                }

                button:hover{
                    background-color: black;
                    color: white;
                    border-radius: 20px;
                }
            }
        }
    }






    iframe{
        height: 100%;
        width: 100%;
    }

    .gmap_canvas {
        overflow:hidden;
        background:none!important;
        height:100%;
        width:100%;
    }

    .mapouter{
        position:relative;
        height:100%;
        width:100%;
    }



    .footer {
        position: relative;
        background-color: var(--Traver5);
        display: flex;
        color: white;
        justify-content: center;
        align-items: center;
        align-content: center;
        height: 4rem;

        .instagram{
            height: 2rem;
            width: 2rem;
            position: absolute;
            right: 1.5rem;
            filter: invert(100%);
            cursor: pointer;
            
        }
    }










    //Phone
    @media only screen and (max-width: 1000px) {
        .container {
            height: 88vh;
            width: 100%;
            display: grid; 
            grid-template-columns: 1fr; 
            grid-template-rows: 1fr 0.5fr 0.5fr ; 
            gap: 0px 0px; 
            grid-template-areas: 
                "form"
                "map"
                "editor";
                 
        

            .editor {
                grid-area: editor;
                background-image: url("/TraverWork.webp");

                .EditorContent{
                    width: 100%;
                    height: 100%;
                    background-color: white;
                    mix-blend-mode: screen;
                    @include FlexCenter;

                    img{
                        display: none;
                    }

                    h2{
                        text-align: center;
                        margin: 0;
                        font-weight: 900;
                        font-size: 1.7rem;
                    }

                    button{
                        margin-top: 1rem;
                        width: 100%;
                        border: 4px solid black;
                        padding: 0.7rem;
                        font-size: 1.4rem;
                        font-family: 'Poppins', sans-serif;
                        background-color: white;
                        border-radius: 50px;
                        font-weight: 900;
                        transition: 700ms;
                        cursor: pointer;
                    }
                }
            }
        }
    }

</style>














<div class="container">

    <div class="form">

        <div class="SuccessBanner" style="transform: translateY(-{SuccessBannerPos}%);">
            <script src="https://cdn.lordicon.com/xdjxvujz.js"></script>
            <lord-icon
                src="https://cdn.lordicon.com/hjeefwhm.json"
                trigger="click"
                colors="primary:#ffffff"
                style="width:30%;height:20%">
            </lord-icon>
            <h2>Messaggio ricevuto, <br> ti risponderemo  presto<br> via Email.</h2>
        </div>



        <h2>Contattaci</h2>
        <form
            method="POST"
            action="https://script.google.com/macros/s/AKfycbwH_R_H6-Dq4f1VLkxikOGwPGwzq2hCLoh5HlYLXhDnnhMhg-B56q3oG-b-4cOA-B2U/exec"

            on:submit|preventDefault={SubmitForm}
            bind:this={form}
        >	
            <input type="text" id="Nome" name="Nome" placeholder="Nome" required>

            
            <input type="text" id="Cognome" name="Cognome" placeholder="Cognome" required>

            
            <input type="text" id="Email" name="Email" placeholder="E-mail" required>

            
            <textarea id="text" name="Messaggio" placeholder="Messaggio" required></textarea>

            <input type="submit" value="Invia" id="SubButt">
        </form>
    </div>

    <div class="map">
        <div class="mapouter">
            <div class="gmap_canvas">
                <iframe title="map" id="gmap_canvas" src="https://maps.google.com/maps?q=41.95208629485354,%2012.75097727097055&t=k&z=15&ie=UTF8&iwloc=&output=embed" frameborder="0" scrolling="no" marginheight="0" marginwidth="0">
                </iframe>
            </div>
        </div>
    </div>

    <div class="editor">
        <div class="EditorContent">
            <img src="logo.svg" alt="logo" />

            <h2>Ordina il tuo <br> travertino personalizzato</h2> 
            
            <a sveltekit:prefetch href="/editor"><button>Apri l'editor</button></a>
        </div>
        
    </div>

</div>


<div class="footer">
        <p>TraverTivoli s.r.l</p>
        <a href="https://instagram.com/travertivoli?igshid=YmMyMTA2M2Y=" class="instagram">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M224.1 141c-63.6 0-114.9 51.3-114.9 114.9s51.3 114.9 114.9 114.9S339 319.5 339 255.9 287.7 141 224.1 141zm0 189.6c-41.1 0-74.7-33.5-74.7-74.7s33.5-74.7 74.7-74.7 74.7 33.5 74.7 74.7-33.6 74.7-74.7 74.7zm146.4-194.3c0 14.9-12 26.8-26.8 26.8-14.9 0-26.8-12-26.8-26.8s12-26.8 26.8-26.8 26.8 12 26.8 26.8zm76.1 27.2c-1.7-35.9-9.9-67.7-36.2-93.9-26.2-26.2-58-34.4-93.9-36.2-37-2.1-147.9-2.1-184.9 0-35.8 1.7-67.6 9.9-93.9 36.1s-34.4 58-36.2 93.9c-2.1 37-2.1 147.9 0 184.9 1.7 35.9 9.9 67.7 36.2 93.9s58 34.4 93.9 36.2c37 2.1 147.9 2.1 184.9 0 35.9-1.7 67.7-9.9 93.9-36.2 26.2-26.2 34.4-58 36.2-93.9 2.1-37 2.1-147.8 0-184.8zM398.8 388c-7.8 19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5 9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7 9-132.1c7.8-19.6 22.9-34.7 42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6 132.1 9c19.6 7.8 34.7 22.9 42.6 42.6 11.7 29.5 9 99.5 9 132.1s2.7 102.7-9 132.1z"/></svg>
        </a>
    </div>