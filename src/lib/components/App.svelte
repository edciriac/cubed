<script>
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
</script>

<div class="wrap">
	<div class="canv" style="height: 50vh;">
	
		<Canvas >
			<Scene content={`<p>hello there!</p>
				<span>I'm a span</span>
				<div>
					<p>kjöafnsdfjlkö</p>
				</div>`}/>
		</Canvas>
	</div>
	
	<div>
		<Canvas>
			<Scene />
		</Canvas>
	</div>
	
	
</div>

<style>
	div{
		position: relative;
  backdrop-filter: blur(5px);
  display: flex;
  color: white;
	}
	
	.wrap{
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	:global(.canv div){
		transition: height 1s ease;		
	}
	
	:global(canvas){
		height: 75vh;
		transition: height 1s ease;
	}
	
</style>