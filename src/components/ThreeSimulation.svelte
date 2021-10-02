<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';

	// Sizing parameters
	export let width = 500;
	export let height = 500;

	// // Observer parameters
	// export let observerDistance;
	// export let observerOrbitalPeriod;

	// // Observee parameters
	// export let observeeDistance;
	// export let observeeOrbitalPeriod;
	// export let observeeSTLFile;
	// export let observeeSize;

	///////////////////////////////////////////////////////////////////////////////////////
	// Visualizer control variables
	///////////////////////////////////////////////////////////////////////////////////////
	// Observer
	let thetaObserver = 0;
	let deltaThetaObserver = 0.01; // Positive value = counter clockwise
	let observerScale = 30;

	// Observee
	let thetaObservee = 0;
	let deltaThetaObservee = 0.05; // Positive value = counter clockwise
	let observeeScale = 50;

	let canvasElement;
	let outputBuffer = new Uint8Array(width * height * 4);
	function sum(prev, curr) {
		return prev + curr;
	}

	let arr = [];

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
		// Observee
		const observee = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x777777 })
		);
		observee.scale.x = 1;
		observee.scale.y = 1;
		observee.scale.z = 1;
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
			observee.rotateY(0.001);

			// Make camera look at observee
			camera.lookAt(observee.position);

			// Render the scene
			renderer.render(scene, camera, reuseableTarget);

			// Process pixels
			gl.readPixels(0, 0, width, height, gl.RGBA, gl.UNSIGNED_BYTE, outputBuffer);

			// Subtract the sum of the alpha values
			lightLevel = outputBuffer.reduce(sum) - width * height * 255;
			arr.push(lightLevel);
			// if (thetaObserver % 2*Math.PI <= 0.5) {console.log(arr)}

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
</script>

View of the asteroid (observee) from earth (observer)
<br />
<canvas bind:this={canvasElement} />
<br />
Light level: {lightLevel}
