<script setup lang="ts">
import { onMounted, onUnmounted, ref, defineExpose } from 'vue'
import * as THREE from 'three'
import catTexture from '@/assets/cat.png'

const container = ref<HTMLElement | null>(null)
let cube: THREE.Mesh
let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let renderer: THREE.WebGLRenderer

function loadTextureAsync(url: string) {
  return new Promise<THREE.Texture>((resolve, reject) => {
    new THREE.TextureLoader().load(url, resolve, undefined, reject)
  })
}

onMounted(async () => {
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  renderer = new THREE.WebGLRenderer({ antialias: true })
  renderer.setSize(window.innerWidth, window.innerHeight)

  if (container.value) {
    container.value.appendChild(renderer.domElement)
  }

  const geometry = new THREE.BoxGeometry(1, 1, 1)
  //const loader = new THREE.TextureLoader()
  const texture = await loadTextureAsync(catTexture)
  texture.anisotropy = renderer.capabilities.getMaxAnisotropy()
  const material = new THREE.MeshBasicMaterial({ map: texture, color: 0xffffff })

  //const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 })
  cube = new THREE.Mesh(geometry, material)
  cube.position.x = 0
  cube.rotation.x = Math.PI / 4
  cube.rotation.y = Math.PI / 4
  scene.add(cube)

  const light = new THREE.PointLight(0xffffff, 1, 100)
  light.position.set(0, 0, 10)
  scene.add(light)

  renderer.render(scene, camera)

  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  // Снимаем слушатель
  window.removeEventListener('resize', handleResize)
})

const randomColor = () => {
  return Math.floor(Math.random() * 0xffffff)
}

const handleResize = () => {
  const width = window.innerWidth
  const height = window.innerHeight

  camera.aspect = width / height
  camera.updateProjectionMatrix()

  renderer.setSize(width, height)
  renderer.render(scene, camera)
}

const rotateOnce = () => {
  // Устанавливаем начальные значения
  const duration = 500 // ms
  const start = performance.now()
  const initialRotationX = cube.rotation.x
  const initialRotationY = cube.rotation.y
  const delta = 0.5 * Math.PI // 90 градусов

  cube.material.color.set(randomColor())

  function animate(time: number) {
    const elapsed = time - start
    const t = Math.min(elapsed / duration, 1) // нормализуем [0,1]

    cube.rotation.x = initialRotationX + delta * t
    cube.rotation.y = initialRotationY + delta * t

    renderer.render(scene, camera)

    if (t < 1) {
      requestAnimationFrame(animate)
    }
  }

  requestAnimationFrame(animate)
}

defineExpose({ rotateOnce })
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
