<template>
  <div class="intro-container w-screen h-screen">
    <!-- * 밤하늘 별 뿌린 느낌의 배경효과 필요 -->
    <canvas ref="canvas" class="fixed top-0 left-0 w-full h-full"></canvas>
    <h1 class="text-9xl">WONNY <br />PORTFOLIO</h1>
    <!-- * 하단 스크롤 효과 필요 -->
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

interface Star {
  x: number
  y: number
  radius: number
  alpha: number
}

interface ShootingStar {
  x: number
  y: number
  length: number
  speed: number
  angle: number
}

const canvas = ref<HTMLCanvasElement | null>(null)
let context: CanvasRenderingContext2D | null = null
let animationFrameId: number

const stars: Star[] = []
const shootingStars: ShootingStar[] = []
const starNum = 200

const random = (min: number, max: number) => Math.random() * (max - min) + min

// 별 초기화
const initStars = (width: number, height: number) => {
  stars.length = 0
  for (let i = 0; i < starNum; i++) {
    stars.push({
      x: random(0, width),
      y: random(0, height),
      radius: random(0.5, 1.5),
      alpha: random(0.3, 1),
    })
  }
}

// 떨어지는 별 생성
const createShootingStar = (width: number) => ({
  x: random(0, width),
  y: random(0, 100),
  length: random(50, 150),
  speed: random(5, 10),
  angle: Math.PI / 45, // 45도
})

// Canvas Resize
const resizeCanvas = () => {
  if (!canvas.value) return
  canvas.value.width = window.innerWidth
  canvas.value.height = window.innerHeight
  initStars(canvas.value.width, canvas.value.height)
}

// 그리기
const draw = () => {
  if (!context || !canvas.value) return

  const { width, height } = canvas.value

  const ctx = context as CanvasRenderingContext2D
  // background
  ctx.fillStyle = '#0b0c2a'
  ctx.fillRect(0, 0, width, height)

  // star
  stars.forEach((star) => {
    ctx.beginPath()
    ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(255, 255, 255, ${star.alpha})`
    ctx.fill()

    // 반짝임
    star.alpha += (Math.random() - 0.5) * 0.05
    star.alpha = Math.min(Math.max(star.alpha, 0.3), 1)
  })

  // Shooting Star 생성
  if (Math.random() < 0.01 && canvas.value) {
    shootingStars.push(createShootingStar(canvas.value.width))
  }

  // Shooting Star 그리기
  shootingStars.forEach((star, index) => {
    ctx.beginPath()
    ctx.moveTo(star.x, star.y)
    ctx.lineTo(
      star.x - star.length * Math.cos(star.angle),
      star.y - star.length * Math.sin(star.angle),
    )
    ctx.strokeStyle = 'white'
    ctx.lineWidth = 1.2
    ctx.stroke()

    star.x += star.speed * Math.cos(star.angle)
    star.y += star.speed * Math.sin(star.angle)

    if (canvas.value) return
    if (star.x > canvas!.value!.width || star.y > canvas!.value!.height) {
      shootingStars.splice(index, 1)
    }
  })

  animationFrameId = requestAnimationFrame(draw)
}

// Life Cycle
onMounted(() => {
  if (!canvas.value) return

  context = canvas.value.getContext('2d')
  resizeCanvas()
  window.addEventListener('resize', resizeCanvas)
  draw()
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCanvas)
  cancelAnimationFrame(animationFrameId)
})
</script>

<style scoped lang="scss">
div.intro-container {
  padding: 50px 100px;
  canvas {
    display: block;
    z-index: -1;
  }
  h1 {
    line-height: 1.2;
  }
}
</style>
