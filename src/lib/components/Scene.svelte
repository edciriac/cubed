<script>
	// TODO: Add randomness to inital values
	import { T } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { spring, tweened } from 'svelte/motion';
	import { HTML } from '@threlte/extras'
	import { createEventDispatcher } from 'svelte';
	interactivity();
	let scale = spring(1);
	let rotate = tweened(0);
	let posY = tweened(1);
	let rotY = rotate;
	let rotZ = rotate;
	let rotX = rotate;
	export let speed = RandomNumberBetween(800, 1100);
	export let contentToShow = ""
	let expanded = false
	export let content = 
	`
	<article on:pointerenter={handleHover}
			on:pointerleave={handleUnhover}>
				<ul>
					<li>
						<a href="https://github.com/edciriac/edciriac-Proyecto-BD-2022">
							Python Web Scraper project (Spanish)
						</a>
						<ul>
							<li> A Web Scraper project which we did in Chile (unfortunately documentation in spanish and not in english). In short, a script that goes through selected Chilean newspapers sites and extracts some info and stores them in a SQL database.</li>
						</ul>
					</li>
				</ul>
			</article>
	`
	const dispatch = createEventDispatcher();
	function dispatchClick(){
		contentToShow = content
		dispatch('click', {})
	}
	
	/**
	 * @param {number} min
	 * @param {number} max
	 */
	function RandomNumberBetween(min, max) {
  		return Math.random() * (max - min) + min;
	}

	
	/**
	 * @type {number}
	 */
	let handle;
	const tick = () => {
		posY.set(Math.sin(Date.now() / speed) * 0.05 + 1);
		rotY.set(Math.sin(Date.now() / speed + 200) * 0.1);
		rotX.set(Math.sin(Date.now() / speed - 100) * 0.1);
		rotZ.set(Math.sin(Date.now() / speed + 100) * 0.1);
		handle = window.requestAnimationFrame(tick);
	};
	tick();

	let handleHover = () => {	
		rotY.set(0);
		rotX.set(0);
		rotZ.set(0);
		posY.set(1);
		scale.set(1.3);
		cancelAnimationFrame(handle);
	}

	let handleUnhover = () => {
		scale.set(1);
		tick();
	};
	
	let handleClick = (/** @type {{ target: { parentElement: any; }; nativeEvent: { target: { parentElement: any; }; }; }} */ event) => { 
		let parent = event.target? event.target.parentElement : event.nativeEvent.target.parentElement
		console.log(parent)
		console.log(parent.parentElement.parentElement)
		// if (!parent.classList.contains("canv")) {
		// 	parent = parent.parentElement.parentElement
		// }
		// if(!expanded){
		// 	parent.classList.add('expanded');
		// 	// parent.style.position = "sticky"
		// 	// parent.style.height = "50vh"
		// 	// parent.style.top = "0vh"
		// } else {
		// 	parent.classList.remove('expanded');
		// 	// parent.style.position = "sticky"
		// 	// parent.style.height = "100vh"
		// 	// parent.style.top = "50vh"
			
		// }
		// console.log(expanded)
		// expanded = expanded ? false : true
		// console.log(expanded)
	};
	
</script>

<T.Mesh
	position.y={$posY}
	rotation={[$rotY, $rotX, $rotZ]}
	scale={$scale}
	on:pointerenter={handleHover}
	on:pointerleave= {handleUnhover}
	on:click={dispatchClick}
>
	<T.BoxGeometry />
	<T.MeshStandardMaterial color="rgb(18, 176, 187);" />
	<HTML center rotation={[0, -1.5, 0]} 
	>
		<!-- <div class="test" on:pointerenter={handleHover}
		on:pointerleave={handleUnhover}><p>hello there asfas fas fa sfas </p></div> -->

		<div class="container" on:pointerenter={handleHover}
		on:pointerleave={handleUnhover}
		on:click={dispatchClick}
		>
			{@html content}
	
		</div>
	</HTML>
</T.Mesh>
<T.Group >
	<T.PerspectiveCamera
		makeDefault
		position={[-10, 1.5, 1]}
		fov={15}
		on:create={({ ref }) => {
			ref.lookAt(0, 1, 0);
		}}
	/>
</T.Group>

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} />
<T.AmbientLight intensity={0.2} />


<style>
	:global(.expanded) {
		/* width: 50%; */
		min-height: 100vh;
		position: sticky;
		top: 0;
	}
	
	.container{
		background-color: rgba(240, 248, 255, 0.609);
		min-width: 50vw;
		padding: 0.5em 0.5em;
		border-radius: 5px;
	}

	:global(.container *){
		color: black;
		pointer-events: none;
	}
	
	:global(article ul){
		padding: 0.5em 1em;
	}
	:global(article li){
		padding: 0;
		margin: 0;
		list-style: circle;
		color: black;
	}
	:global( p){
		padding: 0;
		margin: 0;
	}
</style>