<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';
	import { OBJLoader } from '../../node_modules/three/examples/jsm/loaders/OBJLoader.js';

	// Sizing parameters
	export let width = 500;
	export let height = 500;

	// Observer parameters
	export let observerDistance;
	export let observerOrbitalPeriod;

	// Observee parameters
	export let observeeDistance;
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
	let observerScale = observerDistance * 20;

	// Observee
	let thetaObservee = 0;
	let deltaThetaObservee = 1 / observeeOrbitalPeriod / 100; // Positive value = counter clockwise
	let observeeScale = observeeDistance * 20;

	let canvasElement;
	let outputBuffer = new Uint8Array(width * height * 4);
	function sum(prev, curr) {
		return prev + curr;
	}

	export let lightLevelArray = [];
	export let lightLevel = 0;

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
		camera.position.z = observerScale;
		camera.add(light); // Add light to camera
		scene.add(camera); // Add camera to scene

		///////////////////////////////////////////////////////////////////////////////////////
		// Processing pass setup
		///////////////////////////////////////////////////////////////////////////////////////
		const reuseableTarget = new THREE.WebGLRenderTarget(width, height);
		const gl = renderer.getContext();

		///////////////////////////////////////////////////////////////////////////////////////
		// Object Creation
		///////////////////////////////////////////////////////////////////////////////////////
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
				camera.position.x = observerScale * Math.cos(thetaObserver);
				camera.position.z = -1 * observerScale * Math.sin(thetaObserver);

				thetaObservee += deltaThetaObservee;
				observee.position.x = observeeScale * Math.cos(thetaObservee);
				observee.position.z = -1 * observeeScale * Math.sin(thetaObservee);
				observee.rotateY((observeeRotationVelocity / 100) * (Math.PI / 180));

				// Make camera look at observee
				camera.lookAt(observee.position);

				// Render the scene
				renderer.render(scene, camera, reuseableTarget);

				// Process pixels
				gl.readPixels(0, 0, width, height, gl.RGBA, gl.UNSIGNED_BYTE, outputBuffer);

				// Subtract the sum of the alpha values
				lightLevel = outputBuffer.reduce(sum) - width * height * 255;
				lightLevelArray.push(lightLevel);
				// if (thetaObserver % 2*Math.PI <= 0.5) {console.log(lightLevelArray)}

				// Check to see if any of the alhpa values are less than 255
				// outputBuffer.forEach((e, i) => {
				// 	if ((i+1)%4 == 0){
				// 		if(e!=255){
				// 			alert("Alpha value less than 255")
				// 		}
				// 	}
				// });
			}
			animate();
		});
	});
</script>

<div class="mx-12 flex flex-col items-center bg-blue-100 shadow-md rounded px-8 pt-6 pb-8 mb-4">
	Observer's view
	<br>This is the view that is used to calculate the light curve (shown below).
	<canvas bind:this={canvasElement} />
</div>
