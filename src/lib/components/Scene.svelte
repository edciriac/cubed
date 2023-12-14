<script>
	import { T, useFrame, useTask } from '@threlte/core';

	let posY = 0;
	let posX = 0;
	let rotY = 0;
	let rotX = 0;
	let handle;
	const tick = () => {
		posY = Math.sin(Date.now() / 900) * 0.05 + 1;
		// posX = Math.cos(Date.now() / 1500) * 0.025;
		rotY = Math.sin(Date.now() / 1100) * 0.1;
		rotX = Math.sin(Date.now() / 900) * 0.1;
		handle = window.requestAnimationFrame(tick);
	};
	tick();
</script>

  <T.Mesh position.y={posY} position.x={posX} rotation.y={rotY} rotation.x={rotX}>
    <T.BoxGeometry />
    <T.MeshStandardMaterial color="#0059BA" />
  </T.Mesh>
<T.Group>
	<T.PerspectiveCamera
		makeDefault
		position={[-10, 2.5, 1]}
		fov={15}
		on:create={({ ref }) => {
			ref.lookAt(0, 1, 0);
		}}
	/>
</T.Group>

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} />
<T.AmbientLight intensity={0.2} />
