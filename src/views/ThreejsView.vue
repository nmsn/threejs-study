<script setup lang="ts">
import { onMounted } from 'vue';
import * as THREE from "three"

const init = () => {
  const canvas = document.querySelector('#three')!;
  console.log(canvas);
  const renderer = new THREE.WebGLRenderer({ antialias: true, canvas });
  
  const fov = 75;
  const aspect = 2;  // 相机默认值
  const near = 0.1;
  const far = 5;
  const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
  
  camera.position.z = 2;

	const scene = new THREE.Scene();
  
  // {

    const color = 0xFFFFFF;
    const intensity = 3;
    const light = new THREE.DirectionalLight( color, intensity );
    light.position.set( - 1, 2, 4 );
    scene.add( light );

  // }

	const boxWidth = 1;
	const boxHeight = 1;
	const boxDepth = 1;
	const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);

	const material = new THREE.MeshPhongMaterial( { color: 0x44aa88 } ); // greenish blue
  
	const cube = new THREE.Mesh(geometry, material);
	scene.add(cube);
  
  const render = (time: number) => {
    time *= 0.001;  // 将时间单位变为秒
    cube.rotation.x = time;
    cube.rotation.y = time;

    renderer.render(scene, camera);

    requestAnimationFrame(render);
  };

	requestAnimationFrame( render );

};



onMounted(() => {
  init();
});
</script>

<template>
  <div class="three">
    <canvas id="three"/>
  </div>
</template>

<style>
.three {
  /* min-height: 100vh; */
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 2rem;
}

#three {
  width: 300px;
  height: 150px;
}
</style>
