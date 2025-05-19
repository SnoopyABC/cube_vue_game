<script setup lang="ts">
import { onMounted, onUnmounted, ref, defineExpose, watch } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'
import computerTexture from '@/assets/MagicCat.glb'

const container = ref<HTMLElement | null>(null)
const isAnimated = ref(false)
let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let renderer: THREE.WebGLRenderer
let model: THREE.Object3D
let controls: OrbitControls

const clock = new THREE.Clock()

onMounted(async () => {
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 1

  renderer = new THREE.WebGLRenderer({ antialias: true })
  renderer.setSize(window.innerWidth, window.innerHeight)

  if (container.value) {
    container.value.appendChild(renderer.domElement)
  }

  const loader = new GLTFLoader()
  const gltf = await new Promise<THREE.GLTF>((resolve, reject) =>
    loader.load(computerTexture, resolve, undefined, reject),
  )

  model = gltf.scene
  model.scale.set(0.5, 0.5, 0.5)
  model.position.set(0, 0, 0)
  model.rotation.y = -45
  scene.add(model)

  controls = new OrbitControls(camera, renderer.domElement)
  controls.target.set(0, 0.0, 0)
  controls.update()
  controls.enablePan = false
  controls.enableDamping = true

  const ambient = new THREE.AmbientLight(0xffffff, 0.4)
  const point = new THREE.PointLight(0xffffff, 0.8)
  point.position.set(2, 2, 2)
  scene.add(ambient, point)

  window.addEventListener('resize', handleResize)

  rotateAnimation()

  renderer.render(scene, camera)
})

const animate = () => {
  requestAnimationFrame(animate)
  controls.update()
  renderer.render(scene, camera)
}

const rotateAnimation = () => {
  if (!isAnimated.value) {
    animate()

    return
  }

  requestAnimationFrame(rotateAnimation)

  const delta = clock.getDelta()

  if (model) {
    model.rotation.y += 0.5 * delta
  }

  renderer.render(scene, camera)
}

watch(isAnimated, () => {
  if (isAnimated.value) {
    rotateAnimation()
  }
})

const toggleRotateAnimation = () => {
  isAnimated.value = !isAnimated.value
}

function rotateOnce() {
  if (model) {
    model.rotation.y += 0.5
  }

  renderer.render(scene, camera)
}

onUnmounted(() => {
  // Снимаем слушатель
  window.removeEventListener('resize', handleResize)
})

const handleResize = () => {
  const width = window.innerWidth
  const height = window.innerHeight

  camera.aspect = width / height
  camera.updateProjectionMatrix()

  renderer.setSize(width, height)
  renderer.render(scene, camera)
}

defineExpose({ rotateOnce, toggleRotateAnimation })
</script>

<template>
  <div ref="container" class="three-container"></div>
</template>

<style scoped>
.three-container {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
canvas {
  display: block;
}
</style>
