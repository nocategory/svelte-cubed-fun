<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import { onMount } from 'svelte';

	let spin = 0;

	SC.onFrame(() => {
		spin += 0.01;
	});

	const textureLoader = new THREE.TextureLoader();
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<SC.Canvas
	antialias
	background={new THREE.Color('rgb(20, 10, 20)')}
	fog={new THREE.FogExp2('#fff', 0.1)}
	shadows
>
	<SC.Mesh
		geometry={new THREE.SphereGeometry(1, 32, 32)}
		material={new THREE.MeshStandardMaterial({
			map: textureLoader.load('/earth.jpeg'),
			shininess: 100,
			opacity: 0.5,
			transparent: true
		})}
		position={[0, 0, 0]}
		rotation={[0, 0, spin]}
	/>
	} rotation={[0, spin, 0]} castShadow />
	<SC.PerspectiveCamera position={[5, 1, 2]} />
	<SC.OrbitControls enableZoom maxPolarAngle={Math.PI * 0.51} />
	<SC.AmbientLight intensity={0.7} />
	<SC.DirectionalLight intensity={0.2} position={[-5, 10, 2]} shadow={{ mapSize: [2048, 2048] }} />
	<SC.Group position={[0, -1, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(50, 50)}
			material={new THREE.MeshStandardMaterial({ color: '#d4d4d4' })}
			rotation={[-Math.PI / 2, 0, 0]}
			receiveShadow
		/>

		<SC.Primitive
			object={new THREE.GridHelper(50, 50, 0x444444, 0x555555)}
			position={[0, 0.001, 0]}
		/>
	</SC.Group>
</SC.Canvas>
