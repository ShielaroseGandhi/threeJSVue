<template>
  <div id="container"></div>
</template>

<script>
import * as THREE from "three";

export default {
  name: "Three",
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null
    };
  },
  methods: {
    init: function() {
      let container = document.getElementById("container");

      const fov = 75;
      const width = container.clientWidth;
      const height = container.clientHeight;
      const aspect = width / height;
      const near = 0.01;
      const far = 10;

      // CREATE CAMERA
      this.camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
      this.camera.position.z = 5;

      // CREATE SCENE
      this.scene = new THREE.Scene();

      // CREATE SHAPE
      const boxWidth = 1;
      const boxHeight = 1;
      const boxDepth = 1;

      let geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);
      let material = new THREE.MeshPhongMaterial({ color: 0xffff00 });

      // CREATE MESH
      this.mesh = new THREE.Mesh(geometry, material);
      this.scene.add(this.mesh);

      // ADD LIGHTING
      let light = new THREE.DirectionalLight(0xffffff, 1);
      light.position.set(-2, 2, 5);
      this.scene.add(light);

      // CREATE RENDERER
      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(width, height);
      container.appendChild(this.renderer.domElement);
    },
    animate: function() {
      requestAnimationFrame(this.animate);
      this.mesh.rotation.x += 0.01;
      this.mesh.rotation.y += 0.02;
      this.renderer.render(this.scene, this.camera);
    }
  },
  mounted() {
    this.init();
    this.animate();
  }
};
</script>

<style lang="scss" scoped>
#container {
  height: 100vh;
  width: 100%;
}
</style>
