<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';
	import { OBJLoader } from '../../node_modules/three/examples/jsm/loaders/OBJLoader.js';

	// Sizing parameters
	export let width = 500;
	export let height = 500;

	// Observer parameters
	export let observerOrbitalPeriod;

	// Observee parameters
	export let observeeOrbitalPeriod;
	export let observeeRotationVelocity;
	export let observeeFile;
	export let observeeObjScale;

	///////////////////////////////////////////////////////////////////////////////////////
	// Visualizer control variables
	///////////////////////////////////////////////////////////////////////////////////////
	// Observer
	let thetaObserver = 0;
	let deltaThetaObserver = 1 / observerOrbitalPeriod / 100; // Positive value = counter clockwise
	let observerScale = 20;

	// Observee
	let thetaObservee = 0;
	let deltaThetaObservee = 1 / observeeOrbitalPeriod / 100; // Positive value = counter clockwise
	let observeeScale = 50;

	let canvasElement;

	onMount(() => {
		///////////////////////////////////////////////////////////////////////////////////////
		// THREE.js Setup
		///////////////////////////////////////////////////////////////////////////////////////
		// Create the renderer
		// and append it to the page
		const renderer = new THREE.WebGLRenderer({ antialias: true, canvas: canvasElement });
		renderer.setSize(width, height);

		// Create scene, camera, and light
		const scene = new THREE.Scene();
		const light = new THREE.PointLight(0xffffff, 1, Infinity);
		const camera = new THREE.PerspectiveCamera(75, width / height, 1, 1000);
		camera.position.z = 75;
		camera.add(light); // Add light to camera
		scene.add(camera); // Add camera to scene

		///////////////////////////////////////////////////////////////////////////////////////
		// Object Creation
		///////////////////////////////////////////////////////////////////////////////////////
		// Sun
		const sun = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0xc29e00 })
		);
		sun.scale.x = 7;
		sun.scale.y = 7;
		sun.scale.z = 7;
		scene.add(sun); // Add Sun to scene

		// Observer
		const observer = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x0000ff })
		);
		observer.scale.x = 1;
		observer.scale.y = 1;
		observer.scale.z = 1;
		scene.add(observer); // Add observer to scene

		const loader = new OBJLoader();
		loader.load(`/obj_models/${observeeFile}`, function (observee) {
			// const observee = new THREE.Mesh(geometry, new THREE.MeshPhongMaterial({ color: 0x777777 }));
			observee.scale.x = observeeObjScale;
			observee.scale.y = observeeObjScale;
			observee.scale.z = observeeObjScale;
			scene.add(observee); // Add observee to scene

			///////////////////////////////////////////////////////////////////////////////////////
			// Animation Loop
			///////////////////////////////////////////////////////////////////////////////////////
			function animate() {
				requestAnimationFrame(animate);

				// Logic goes here
				thetaObserver += deltaThetaObserver;
				observer.position.x = observerScale * Math.cos(thetaObserver);
				observer.position.y = observerScale * Math.sin(thetaObserver);

				thetaObservee += deltaThetaObservee;
				observee.position.x = observeeScale * Math.cos(thetaObservee);
				observee.position.y = observeeScale * Math.sin(thetaObservee);
				observee.rotateZ((observeeRotationVelocity / 100) * (Math.PI / 180));

				// Render the scene
				renderer.render(scene, camera);
			}
			animate();
		});
	});
</script>

<div class="mx-12 flex flex-col items-center bg-blue-100 shadow-md rounded px-8 pt-6 pb-8 mb-4">
	<div class="max-w-sm">
		<b>Overall/Positional view</b>
		<br />This view approximates where the two objects are relative to each other and the sun.
	</div>
	<canvas bind:this={canvasElement} />
</div>
