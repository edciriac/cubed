<script>
	import { T } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { spring, tweened } from 'svelte/motion';
	import { HTML } from '@threlte/extras'
	interactivity();
	let scale = spring(1);
	let rotate = tweened(0);
	let posY = tweened(1);
	let rotY = rotate;
	let rotZ = rotate;
	let rotX = rotate;
	let speed = 900;
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
</script>

<T.Mesh
	position.y={$posY}
	rotation={[$rotY, $rotX, $rotZ]}
	scale={$scale}
	on:pointerenter={() => {
		rotY.set(0);
		rotX.set(0);
		rotZ.set(0);
		posY.set(1);
		scale.set(1.3);
		cancelAnimationFrame(handle);
	}}
	on:pointerleave={() => {
		scale.set(1);
		tick();
	}}
>
	<T.BoxGeometry />
	<T.MeshStandardMaterial color="#0059BA" />
	<HTML transform rotation={[0, -1.5, 0]} >
		<div class="test"><p>hello there asfas fas fa sfas </p></div>
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
	.test{
		position: absolute;
		width: 100%;
		height: 100%;
		background-color: rgba(0,0,0,0.3);
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
		pointer-events: none;
	}
</style>