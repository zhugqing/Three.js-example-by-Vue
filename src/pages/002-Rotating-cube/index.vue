<template>
  <div class="home">
    <canvas id="square" width="800" height="800"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'RotatingCubePage',
  components: {
  },
  mounted() {
    this.main()
  },
  methods: {
    main() {

      const canvas = document.getElementById('square');
      const renderer = new THREE.WebGLRenderer({canvas});

      // 相机 camera
      const fov = 75;
      const aspect = 1;
      const near = 0.1;
      const far = 5;
      const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
      camera.position.z = 2.5;

      // 场景
      const scene = new THREE.Scene();
      const w = 1;
      const h = 1;
      const d = 1;
      const geometry = new THREE.BoxGeometry(w, h ,d);
      const material = new THREE.MeshBasicMaterial({color: 'skyblue'}); // MeshBasicMaterial材质不受光照影响
      const cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      // 调用渲染函数
      renderer.render(scene, camera);

      // 让立方体旋转
      function render(time) {
        time *= 0.001;
        cube.rotation.x = time;
        cube.rotation.y = time;
        renderer.render(scene, camera);
        requestAnimationFrame(render);
      }
      requestAnimationFrame(render);
    },
  }
}
</script>
