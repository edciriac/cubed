<script>
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
</script>

<div class="wrap">
	<div>
	
		<Canvas >
			<Scene />
		</Canvas>
	</div>
	
	<div>
		<Canvas>
			<Scene />
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
		height: 50vh;
  backdrop-filter: blur(5px);
  display: flex;
  color: white;
	}
	
	.wrap{
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}
</style>