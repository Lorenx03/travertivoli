<script>
	import { fade } from 'svelte/transition';
    import { onMount } from 'svelte';
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import Block from '$lib/block.svelte';
	import CartItem from '$lib/CartComponents/CartItem.svelte';


    let texture;

    onMount(()=> {
         texture = new THREE.TextureLoader().load('/TraverTexure.jpg');
    });

	let OpenCart = false;

    let width = 100;
	let height = 50;
	let depth = 100;

	let widthReduced = 1;
	let heightReduced = 1;
	let depthReduced = 1;

	$:widthReduced = width/100;
	$:heightReduced = height/100;
	$:depthReduced = depth/100;
	

	let quantity = 1;
	let color = 0;
	let price = 3000;

	let TraverClick = "Classico";

	let currentPrice = 0;
	$:currentPrice = widthReduced*heightReduced*depthReduced*price;


	let Orders = [];
	let CurrentId = 0;

	let Total = 0;
	
	function AddToCart() {
		
		OrderSuccess = true;
		Orders[CurrentId] = {
			id: CurrentId,
			color: color,
			X: width,
			Y: depth,
			Z: height,
			n: quantity,
			price: currentPrice*quantity
		};
		CurrentId++;

		Total = Total + currentPrice*quantity;
		console.log(Orders);

		setTimeout(() => {
			OrderSuccess = false;

			width = 100;
			height = 50;
			depth = 100;
			quantity = 1;
			color = 0;
			price = 3000;
			SetClassic();
		}, 1000);
	}


	

	let Showred = false;
	function RemoveOrder(id) {
		Showred = true;
		setTimeout(() => {
			Total = Total - Orders[id].price; 

			Orders.splice(id,1);

			for (let i = 0; i < Orders.length; i++) {
				Orders[i].id = i;
			}

			CurrentId--;
		}, 500);

		setTimeout(() => {
			ReRender();
		}, 1000);

		setTimeout(() => {
			ReRender();
			Showred = false;
		}, 1200);
	}



	let OrderSuccess = false;

	
	let spin = 0;

	SC.onFrame(() => {
		spin += 0.001;
	});

	function SetClassic() {
		texture = new THREE.TextureLoader().load('/TraverTexure.jpg');
		price = 3000;
		color = 0;
		TraverClick = "Classico";
	}

	function SetNavona() {
		texture = new THREE.TextureLoader().load('/Travertino-Navona.jpg');
		price = 4000;
		color = 1;
		TraverClick = "Navona";
	}

	function SetNoce() {
		texture = new THREE.TextureLoader().load('/travertino-noce.jpg');
		price = 4500;
		color = 2;
		TraverClick = "Noce";
	}

	function SetSilver() {
		texture = new THREE.TextureLoader().load('/TravertinoSilver.webp');
		price = 5000;
		color = 3;
		TraverClick = "Silver";
	}

	function SetAlabastrino() {
		texture = new THREE.TextureLoader().load('/TravertinoAlabastrino.webp');
		price = 6000;
		color = 4;
		TraverClick = "Alabastrino";
	}

	function virgola(x) {
    	var parts = x.toString().split(".");
    	parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    	return parts.join(".");
	}

	let bool = true;
	let test;
	function ReRender(){
		
		if(bool)
		{
			test = CurrentId;
			bool = false
			CurrentId = 0;
		}else
		{
			bool = true;
			CurrentId = test;
		}
		
	}

	let FormY = 100;
	let RedirectY = 100;

	let countdown = 10;
	function SubmitForm() {
		RedirectY = 0;

		setInterval(() => {
			countdown--;
		}, 1000);
	}

	$:if(countdown == 0)
			window.location.href = "/";
</script>




<style lang="scss">
	input[type=number]::-webkit-inner-spin-button,
	input[type=number]::-webkit-outer-spin-button { 
      -webkit-appearance: none; 
      margin: 0;
	}

	.QNumber{
		font-family: 'Poppins', sans-serif;
		font-size: 2rem;
		text-align: center;
		border: 1px solid rgba(0, 0, 0, 0.116);
		border-radius: 10px;
		width: 3rem;
	}

	button:hover{
		transform: scale(1.1);
		box-shadow: 0px 5px 8px #00000052;
	}

	button:active{
		transform: scale(1) translateY(0.3rem);
	}
	
	.editor{
		height: 100vh;
		width: 100%;
		background-color: white;

		.scene{
			position: relative;
			height: 67vh;
			border-radius: 0 0 20px 20px;
			overflow: hidden;
			background-image: url('/TraverWorkBlur.webp');
			background-position: center;
		}


		.bottomPane{
			position: fixed;
			height: 33vh;
			width: 100%;
			bottom: 0;
			display: flex;
			justify-content: center;


			.TraverType{
				div{
					display: flex;

					div{
						 display: flex; 
						 flex-direction: column;
						 align-items: center;
						 margin: 0.5rem;
						 padding: 0.5rem;
						 box-shadow: 0px 5px 8px #00000057;
						 border-radius: 10px;
					}

					button{
						padding: 0;
						margin-bottom: 0.3rem;
						border-radius: 10px;
						overflow: hidden;
						height: 3rem;
						width: 3rem;
						border-width: 0;
						cursor: pointer;
						transition: 100ms;

						img{
							height: 3rem;
							width: 3rem;
						}
					}
				}
			}


			.TraverDim{
				label{
					margin: 0.5rem;
					

					span{
						width: rem;
					}

					input[type=number]{
						font-family: 'Poppins', sans-serif;
						font-size: 1rem;
						text-align: center;
						border: 1px solid rgba(0, 0, 0, 0.116);
						border-radius: 10px;
						width: 3rem;
					}
				}
			}


			.TraverTot{
				min-width: 600px!important;

				button{
					width: 40%;
                    border: 2px solid var(--Traver5);
                    padding: 0.5rem;
                    font-size: 1rem;
                    font-family: 'Poppins', sans-serif;
                    background-color: white;
                    border-radius: 50px;
                    font-weight: 900;
                    transition: 400ms;
                    cursor: pointer;
				}

				button:hover{
                    background-color: var(--Traver5);
                    color: white;
                    border-radius: 10px;
                }

				h1{
					margin: 1rem 0;
					display: flex;
					align-items: center;

					div{
					display: flex;
					flex-direction: column;
					margin-left: 0.1rem;

						button{
						width: 1.5rem;
						height: 1.5rem;
						display: flex;
						align-items: center;
						justify-content: center;
						border: 2px solid var(--Traver5);
						padding: 0.5rem;
						font-size: 1rem;
						font-family: 'Poppins', sans-serif;
						background-color: white;
						border-radius: 50px;
						font-weight: 900;
						transition: 400ms;
						cursor: pointer;
						margin: 0.1rem;
					}
				}
				}

				
			}

			.bottomThird{
				width: 30%;
				display: flex;
				align-items: center;
				justify-content: flex-start;
				align-content: center;
				flex-direction: column;
				flex-wrap: nowrap;
				margin-top: 1.5rem;

				h2{
					margin: 0;
				}
			}
		}
	}


	.ShoppingCart{
		position: fixed;
		top: 1rem;
		right: 1rem;
		background-color: white;
		display: flex;
		padding: 0.5rem;
		border-radius: 100px;

		h2{
			margin: 0;
			padding: 0 1rem;
			text-align: center;
			display: flex;
			align-items: center;
			justify-content: center;
		}

		.icon{
			background-color: var(--Traver5);
			display: flex;
			align-items: center;
			justify-content: center;
			width: 2.5rem;
			height: 2.5rem;
			border-radius: 50%;
			cursor: pointer;
		}
	}


	.home{
		position: fixed;
		top: 1rem;
		left: 1rem;
		background-color: var(--Traver5);
		display: flex;
		padding: 0.5rem;
		border-radius: 100px;
		border: 0.3rem solid white;
		cursor: pointer;
	}



	.OrderSuccess{
		width: 100%;
		position: fixed;
		top: 0;
		height: 100%;
		background-color: var(--Traver5);
		z-index: 9999;
		display: flex;
		align-items: center;
		justify-content: center;
		opacity: 1;

		h1{
			color: white;
			font-size: 5rem;
			text-align: center;
		}
	}



	.CartTitle{
		width: 100%;
		background-image: url('/TraverWork.webp');
		border-radius: 0 0 0px 20px;
		height: 10vh;
		display: flex;
		align-items: center;
		justify-content: center;

		h1{
			color: white;
			margin: 0;
			font-size: 4rem;
			text-align: center;
		}

		div{
			color: white;
			width: 1.5rem;
			height: 1.5rem;
			filter: invert(100%);
			position: absolute;
			left: 2rem;
			top: 1.4rem;
			cursor: pointer;
		}
	}

	.CartContent{
		width: 100%;
		height: 80vh;
		overflow-y: scroll;
		
		
		h1{
			color: rgba(0, 0, 0, 0.281);
			font-size: 2.5rem;
			text-align: center;
		}
	}

	.CartBottom{
		width: 100%;
		height: 5rem;
		background-color: var(--Traver5);
		height: 10vh;
		border-radius: 20px 0 0px 0px;
		display: flex;
		align-items: center;
		z-index: 9999;

		h1{
			color: white;
			margin: 0;
			margin-left: 2rem;
			font-size: 2rem;
		}

		.Ordina{
			background-color: var(--Traver4);
			position: absolute;
			right: 0;
			bottom: 0;
			padding: 1rem 4rem;
			border-radius: 50px 0 0px 0px;
			transition: 400ms;
			cursor: pointer;

			span{
				color: white;
				margin: 0;
				font-size: 4rem;
			}
		}

		.Ordina:hover{
			background-color: var(--Traver3);
			transform: scale(1.1);
		}
	}


	.CartItemClass{
		position: relative;
		.DeleteButt{
			height: 2rem;
			width: 2rem;
			position: absolute;
			right: 2rem;
			top: 3.5rem;
			filter: invert(17%) sepia(46%) saturate(7484%) hue-rotate(356deg) brightness(107%) contrast(132%);
			opacity: 0;
			transition: 300ms;
			cursor: pointer;
		}
	}


	.CartItemClass:hover{
		.DeleteButt{
			opacity: 1;
		}
	}


	.red{
		position: fixed;
		width: 100%;
		height: 100%;
		top: 0;
		background-color: rgb(146, 0, 0);
		z-index: 9999;
		display: flex;
		align-items: center;
		justify-content: center;

		h1{
			color: white;
			font-size: 3rem;
		}
	}


	//Br totale carrello
	.BRtot{
		display: none;
	}
	


	/* width */
	::-webkit-scrollbar {
	width: 5px;
	}

	/* Track */
	::-webkit-scrollbar-track {
	background: white; 
	}
	
	/* Handle */
	::-webkit-scrollbar-thumb {
	background: var(--Traver4); 
	}

	/* Handle on hover */
	::-webkit-scrollbar-thumb:hover {
	background: var(--Traver5); 
	}














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

	.OrderConfirm{
		height: 100%;
		width: 100%;
		background-color: rgba(0, 0, 0, 0.726);
		position: fixed;
		z-index: 9999;
		backdrop-filter: blur(8px);
		display: flex;
		align-items: center;
		justify-content: center;
		transition: 500ms;


		.CloseForm{
			height: 100%;
			width: 100%;
			position: fixed;
			z-index: 999;
			cursor: pointer;
		}

		.form {
            padding: 2rem 3rem;
            grid-area: form;
            background-color: white;
			border-radius: 50px;
			z-index: 1000;
            
            @include FlexCenter;

            h2{
                margin: 0;
                color: var(--Traver5);
                font-size: 3rem;
            }

			p{
				margin: 0.5rem 0;
				text-align: center
			}
            
            form{
                @include FlexCenter;
				margin-top: 0.5rem;

                input{
                    @include formStyles;
                }

                input:focus{
                   border-radius:10px;
                   min-width: 60%;
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
	}







	.Redirect{
		position: fixed;
		width: 100%;
		height: 100%;
		top: 0;
		background-color: var(--Traver5);
		z-index: 99999;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		color: white;
		transition: 500ms;
		text-align: center;

		h1{
			margin-bottom: 0;
			font-size: 3rem;
		}
	}






























	@media only screen and (max-width: 1000px) {
			.editor{
			height: 100vh;
			width: 100%;
			background-color: white;

			.scene{
				position: relative;
				height: 36vh;
				border-radius: 0 0 20px 20px;
				overflow: hidden;
				background-image: url('/TraverWorkBlur.webp');;
			}


			.bottomPane{
				position: relative;
				height: 60vh;
				width: 100%;
				/*bottom: 0;*/
				overflow: auto;
				display: flex;
				justify-content: flex-start;
				flex-direction: column;
				align-content: center;
				align-items: center;
				flex-wrap: nowrap;
				


				.TraverType{
					div{
						display: flex;

						div{
							display: flex; 
							flex-direction: column;
							align-items: center;
							margin: 0.5rem;
							padding: 0.5rem;
							box-shadow: 0px 5px 8px #0000001a;
							border-radius: 10px;
						}

						button{
							padding: 0;
							margin-bottom: 0.3rem;
							border-radius: 10px;
							overflow: hidden;
							height: 3rem;
							width: 3rem;
							border-width: 0;
							cursor: pointer;
							transition: 100ms;

							img{
								height: 3rem;
								width: 3rem;
							}
						}
					}
				}


				.TraverDim{
					label{
						margin: 0.5rem;
						

						span{
							width: rem;
						}

						input[type=number]{
							font-family: 'Poppins', sans-serif;
							font-size: 1rem;
							text-align: center;
							border: 1px solid rgba(0, 0, 0, 0.116);
							border-radius: 10px;
							width: 3.5rem;
						}
					}
				}


				.TraverTot{
					button{
						width: 40%;
						border: 2px solid var(--Traver5);
						padding: 0.5rem;
						font-size: 1rem;
						font-family: 'Poppins', sans-serif;
						background-color: white;
						border-radius: 50px;
						font-weight: 900;
						transition: 400ms;
						cursor: pointer;
					}

					button:hover{
						background-color: var(--Traver5);
						color: white;
						border-radius: 10px;
					}

					h1{
						margin: 1rem 0;
						display: flex;
						align-items: center;

						div{
						display: flex;
						flex-direction: column;
						margin-left: 0.1rem;

							button{
							width: 1.5rem;
							height: 1.5rem;
							display: flex;
							align-items: center;
							justify-content: center;
							border: 2px solid var(--Traver5);
							padding: 0.5rem;
							font-size: 1rem;
							font-family: 'Poppins', sans-serif;
							background-color: white;
							border-radius: 50px;
							font-weight: 900;
							transition: 400ms;
							cursor: pointer;
							margin: 0.1rem;
						}
					}
					}

					
				}

				.bottomThird{
					width: 100%;
					display: flex;
					align-items: center;
					justify-content: center;
					align-content: center;
					flex-direction: column;
					flex-wrap: nowrap;
					margin-top: 1.5rem;

					h2{
						margin: 0;
					}
				}
			}
		}





			.CartTitle{
			width: 100%;
			background-image: url('/TraverWork.webp');
			border-radius: 0 0 0px 20px;
			height: 7vh;
			display: flex;
			align-items: center;
			justify-content: center;

			h1{
				color: white;
				margin: 0;
				font-size: 4rem;
				text-align: center;
			}

			div{
				color: white;
				width: 1.5rem;
				height: 1.5rem;
				filter: invert(100%);
				position: absolute;
				left: 2rem;
				top: 1.4rem;
				cursor: pointer;
			}
		}

		.CartContent{
			width: 100%;
			height: 77vh;
			overflow-y: scroll;
			
			
			h1{
				color: rgba(0, 0, 0, 0.281);
				font-size: 2.5rem;
				text-align: center;
			}
		}

		.CartBottom{
			width: 100%;
			height: 5rem;
			background-color: var(--Traver5);
			height: 9vh;
			border-radius: 20px 0 0px 0px;
			display: flex;
			align-items: center;
			z-index: 9999;

			h1{
				color: white;
				margin: 0;
				margin-left: 2rem;
				font-size: 2rem;
			}

			.Ordina{
				background-color: var(--Traver4);
				position: absolute;
				right: 0;
				bottom: 7vh;
				padding: 1rem 4rem;
				border-radius: 50px 0 0px 0px;
				transition: 400ms;
				cursor: pointer;

				span{
					color: white;
					margin: 0;
					font-size: 4rem;
				}
			}

			.Ordina:hover{
				background-color: var(--Traver3);
				transform: scale(1.1);
			}
		}

		.red{
			position: fixed;
			width: 100%;
			height: 100%;
			top: 0;
			background-color: rgb(146, 0, 0);
			z-index: 9999;
			display: flex;
			align-items: center;
			justify-content: center;

			h1{
				color: white;
				font-size: 3rem;
			}
		}

		.BRtot{
			display: initial;
		}
	}





















</style>



<svelte:head>
    <title>Editor</title>
</svelte:head>



<div class="Redirect" style="transform: translateY({RedirectY}%);">

	<script src="https://cdn.lordicon.com/xdjxvujz.js"></script>
	<lord-icon
		src="https://cdn.lordicon.com/htdttjjb.json"
		trigger="loop"
		colors="primary:#ffffff"
		style="width:250px;height:250px">
	</lord-icon>

	<h1>Ordine effettuato!</h1>
	<p>Ti abbiamo mandato un' e-mail di conferma, <br> lì troverai il riepilogo, il <b>numero</b> del tuo <b>ordine</b> <br> e il numero telefonico del consulente.
	</p>
	

	<br>
	<br>
	<p>Verrai reindirizzato tra {countdown} secondi...</p>
</div>


<div class="OrderConfirm" style="transform: translateY({FormY}%);">

	<div class="CloseForm" on:click={() => { FormY = 100;}}>
		
	</div>

	<div class="form">
        <h2>Completa ordine</h2>
		<p>Ci siamo quasi, completa il <b>form</b> e <br> ti manderemo una <b>e-mail</b> di conferma.
		</p>
		
		<p>
		Successivamente, potrai metterti d'accordo <br> con il nostro <b>consulente</b> per la modalità <br> di pagamento e consegna.
		</p>
        <form on:submit|preventDefault={SubmitForm}>	
            <input type="text" id="Nome" name="Nome" placeholder="Nome" required>

            
            <input type="text" id="Cognome" name="Cognome" placeholder="Cognome" required>

            
            <input type="text" id="Email" name="Email" placeholder="E-mail" required>

			<input type="text" id="Indirizzo" name="Indirizzo" placeholder="Indirizzo" required>

            <input type="submit" value="Invia" id="SubButt">
        </form>
    </div>
</div>







<Block BackgroudColor='white' Show={OpenCart} from={"Right"} zindex={"1000"}>
    <div class="CartTitle">
		<div on:click={() => {OpenCart = false}}>
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M224 480c-8.188 0-16.38-3.125-22.62-9.375l-192-192c-12.5-12.5-12.5-32.75 0-45.25l192-192c12.5-12.5 32.75-12.5 45.25 0s12.5 32.75 0 45.25L77.25 256l169.4 169.4c12.5 12.5 12.5 32.75 0 45.25C240.4 476.9 232.2 480 224 480z"/></svg>
		</div>
		<h1>
			<script src="https://cdn.lordicon.com/xdjxvujz.js"></script>
			<lord-icon
				src="https://cdn.lordicon.com/aoggitwj.json"
				trigger="hover"
				colors="primary:#ffffff"
				style="width:4rem;height:4rem">
			</lord-icon>
		</h1>
	</div>
	<div class="CartContent">
		{#if Showred == true}
			<div class="red" transition:fade>
				<h1>Eliminando...</h1>
			</div>
		{/if}


		{#if CurrentId == 0}
			<h1 style="margin-top: 6rem;">Carrello vuoto!</h1>
		{:else}
			{#each Orders as order(order.id)}
				<div class="CartItemClass">
					<div class="DeleteButt" on:click={() => {RemoveOrder(order.id)}}>
						<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M310.6 361.4c12.5 12.5 12.5 32.75 0 45.25C304.4 412.9 296.2 416 288 416s-16.38-3.125-22.62-9.375L160 301.3L54.63 406.6C48.38 412.9 40.19 416 32 416S15.63 412.9 9.375 406.6c-12.5-12.5-12.5-32.75 0-45.25l105.4-105.4L9.375 150.6c-12.5-12.5-12.5-32.75 0-45.25s32.75-12.5 45.25 0L160 210.8l105.4-105.4c12.5-12.5 32.75-12.5 45.25 0s12.5 32.75 0 45.25l-105.4 105.4L310.6 361.4z"/></svg>
					</div>

					<CartItem {...order}/>
				</div>
			{/each}
		{/if}
		
	</div>
	<div class="CartBottom">
		<h1>Totale: <br class="BRtot"> {virgola(Total.toFixed(2))}€</h1>
		{#if CurrentId != 0}
			<div class="Ordina" on:click={() => { FormY = 0;}}>
				<span>Ordina</span>
			</div>
		{/if}
	</div>
</Block>



{#if OrderSuccess}
	<div class="OrderSuccess" transition:fade>
		<h1>Aggiunto al carrello!</h1>
	</div>
{/if}




<div class="editor">
	<div class="scene">
		<SC.Canvas antialias alpha={true}>
			<SC.Mesh
				geometry={new THREE.BoxGeometry()}
				material={new THREE.MeshStandardMaterial({ map:texture })}
				scale={[widthReduced, heightReduced, depthReduced]}
				rotation={[0, spin, 0]}
			/>
			<SC.PerspectiveCamera position={[1, 1, 3]} />
			<SC.OrbitControls enableZoom={true} enablePan={false} />
			<SC.AmbientLight intensity={0.6} />
			<SC.DirectionalLight intensity={0.6} position={[2, 3, 2]} />
		</SC.Canvas>
	</div>


	<a href="/" class="home">
		<script src="https://cdn.lordicon.com/xdjxvujz.js"></script>
		<lord-icon
			src="https://cdn.lordicon.com/igpbsrza.json"
			trigger="hover"
			colors="primary:#ffffff"
			state="hover-2"
			style="width:1.4rem;height:1.4rem">
		</lord-icon>
	</a>


	<div class="ShoppingCart">
		<h2>Totale: {virgola(Total.toFixed(2))}€</h2>
		<div class="icon" on:click={() => {OpenCart = true}}>
			<script src="https://cdn.lordicon.com/xdjxvujz.js"></script>
			<lord-icon
				src="https://cdn.lordicon.com/aoggitwj.json"
				trigger="hover"
				colors="primary:#ffffff"
				style="width:1.4rem;height:1.4rem">
			</lord-icon>
		</div>
	</div>
	

	<div class="bottomPane">
		<div class="TraverType bottomThird">
			<h2>Colore:</h2>

			<div>
				<div>
					<button on:click={SetClassic}><img src="/TraverTexure.jpg" alt="traver"></button>
					<span>3k€/m³</span>
				</div>
				
				<div>
					<button on:click={SetNavona}><img src="/Travertino-Navona.jpg" alt="traver"></button>
					<span>4k€/m³</span>
				</div>
				
				<div>
					<button on:click={SetNoce}><img src="/travertino-noce.jpg" alt="traver"></button>
					<span>4.5k€/m³</span>
				</div>

				<div>
					<button on:click={SetSilver}><img src="/TravertinoSilver.webp" alt="traver"></button>
					<span>5k€/m³</span>
				</div>

				<div>
					<button on:click={SetAlabastrino}><img src="/TravertinoAlabastrino.webp" alt="traver"></button>
					<span>6k€/m³</span>
				</div>
			</div>


			<span style="opacity: 0.4; text-align: center;">(il costo di spezione e lavorazione non è incluso nel prezzo)</span>

			<span>{TraverClick}</span>
		</div>

		<div class="TraverDim bottomThird">
			<h2>Dimensioni:</h2>

			<label>
				<span>Y:</span>
				<input type="range" bind:value={width} min={1} max={300} step={0.01} /> 
				<input type="number" min={1} max={300} bind:value={width} step={0.1} />
				cm
			</label>
			<label>
				<span>X:</span>
				<input type="range" bind:value={depth} min={1} max={300} step={0.01} /> 
				<input type="number" min={1} max={300} bind:value={depth} step={0.1} />
				cm
			</label>
			<label>
				<span>Z:</span>
				<input type="range" bind:value={height} min={1} max={150} step={0.01} />
				{#key depth}
				<input type="number" min={1} max={150} bind:value={height} step={0.1}/>
				{/key}
				cm
			</label>
		</div>

		
		<div class="TraverTot bottomThird">
			<h2>Prezzo:</h2>
			<h1>{virgola(currentPrice.toFixed(2))}€ × 

				

				<div style="border: 1px solid rgba(0, 0, 0, 0.116);; padding: 0.3rem; border-radius: 10px">
					<span style="font-weight: 300; font-size: 1rem; text-align:center">n. pezzi</span> 
				
					<div style="flex-direction: row;
    					justify-content: space-evenly;
    					align-content: center;
    					align-items: center;">
						<input type="number" min={1} max={30} bind:value={quantity} step={1} class="QNumber"/> 
						<div>
							<button on:click={() => {(quantity < 30) ? quantity++ : quantity = quantity}}>+</button>
							<button on:click={() => {(quantity > 1) ? quantity-- : quantity = quantity}}>-</button>
						</div>
					</div>
				</div>
				
				
				= {virgola((currentPrice*quantity).toFixed(2))}€
			</h1>
			
			<button on:click={AddToCart}>Aggiungi al carrello</button>
		</div>
		
	</div>
</div>





