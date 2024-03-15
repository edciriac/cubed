<script>
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
	import { onMount } from 'svelte';

	let wrapper
	let old;
	/**
	 * @type {HTMLElement | null}
	 */
	let showbox
	let contentToShow

	let fakeData = [
		{
			"jobTitle" : "Software Engineer",
			"content": "diipadaaba some text here"
		},
		{
		    "jobTitle" : "test job",
			"content": "description of the job here"
		},
		{
			"jobTitle" : "test job 2",
			"content": "description of the job here"
		}
	]

	// const goToShowbox = (event) => {
	// 	console.log("event.target")
	// 	console.log(event.target)
	// 	// wrapper = event.target.parentNode;
	//     
	// 	console.log(wrapper)
	// 	showboxbind.appendChild(wrapper);
		
	
	// }
	/**
	 * @param {any} event
	 */
	function handleClick(event) {
		console.log("click")
		if (showbox) {
			showbox.classList.remove("hide");
		}
	}
	
	onMount(() => {
		let allCanvas = document.getElementsByClassName("canv");
		showbox = document.getElementById("showbox");
		console.log(showbox)
	    // Hide showbox
		showbox.classList.add("hide");
		showbox.addEventListener("click", function(){
            // empty showbox's innerhtml 
            // while(showbox.firstChild){
            //     showbox.removeChild(showbox.firstChild);
            // }
            // showbox.setHTML(""); //Browser doesn't support this line yet
            // make showbox unclickable with adding the hide class to it
            showbox.classList.add("hide");
        })
	})
</script>

<div class="wrap">
	
	{#each fakeData as job}
		<div class="canv" style="height: 50vh;">
			<Canvas>
				<Scene on:click={handleClick} content={`<p>${job.content}</p>`} bind:contentToShow></Scene>
			</Canvas>
			</div>
	{/each}
	

</div>

<div id="showbox">
	<div class="canv" style="height: 50vh; border-style: dotted;border-color: aqua; border-width: 2px;">
		<Canvas>
			<Scene content={contentToShow} />
		</Canvas>
	</div>
</div>

<style>
div{
	/* position: relative; */
	backdrop-filter: blur(5px);
	display: flex;
	color: white;
}
#showbox{
	position: absolute;
	top: 12.5vh;
	left: 12.5vw;
	height: 75vh;
	width: 75vw;
	opacity : 0.7;
	background: rosybrown;
	border: 1px solid black;
	margin: auto;
}		
#showbox>div {
        width: 100%;
        height: 100%;
    }

.wrap{
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
	position: absolute;
}



:global(.canv div){
	transition: height 1s ease;		
}

:global(canvas){
	height: 75vh;
	transition: height 1s ease;
}
:global(.hide){
    display: none !important;
    pointer-events: none;
}
	
</style>