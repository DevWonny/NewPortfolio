<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import { throttle } from 'lodash'
// component
import Intro from '@/components/Intro.vue'
import Introduce from '@/components/Introduce.vue'
import Career from '@/components/Career.vue'
import Project from '@/components/Project.vue'
import Contact from '@/components/Contact.vue'

const introRef = ref()
const introduceRef = ref()
const careerRef = ref()
const projectRef = ref()
const contactRef = ref()

const sections = ref<HTMLElement[]>([])
const currentIndex = ref(0)
let isAnimating = false
let scrollTimeout: number | null = null
let accumulatedDelta = 0
const SCROLL_THRESHOLD = 80 // 해당 값 이상 쌓여야 다음 페이지로 이동

// Smooth Animation
const smoothScrollTo = (targetY: number, duration = 600) => {
  const startY = window.scrollY
  const distance = targetY - startY
  const startTime = performance.now()

  isAnimating = true

  const animation = (currentTime: number) => {
    const elapsed = currentTime - startTime
    const progress = Math.min(elapsed / duration, 1)

    // easeInOutCubic
    const ease =
      progress < 0.5 ? 4 * progress * progress * progress : 1 - Math.pow(-2 * progress * 2, 3) / 2

    window.scrollTo(0, startY + distance * ease)

    if (progress < 1) {
      requestAnimationFrame(animation)
    } else {
      isAnimating = false
    }
  }

  requestAnimationFrame(animation)
}

// Wheel Event
const onWheel = (e: WheelEvent) => {
  e.preventDefault()
  if (isAnimating) return

  accumulatedDelta += e.deltaY

  if (scrollTimeout) clearTimeout(scrollTimeout)

  scrollTimeout = window.setTimeout(() => {
    if (accumulatedDelta > SCROLL_THRESHOLD && currentIndex.value < sections.value.length - 1) {
      currentIndex.value++
    } else if (accumulatedDelta < -SCROLL_THRESHOLD && currentIndex.value > 0) {
      currentIndex.value--
    }

    const target = sections.value[currentIndex.value]
    if (target) {
      const targetY = target.offsetTop
      smoothScrollTo(targetY, 600)
    }

    accumulatedDelta = 0
  }, 100)
}

onMounted(async () => {
  await nextTick()

  sections.value = [
    introRef.value?.$el,
    introduceRef.value?.$el,
    careerRef.value?.$el,
    projectRef.value?.$el,
    contactRef.value?.$el,
  ].filter((el): el is HTMLElement => !!el)

  window.addEventListener('wheel', onWheel, { passive: false })
})

onBeforeUnmount(() => {
  window.removeEventListener('wheel', onWheel)
})
</script>

<template>
  <div class="app-container">
    <Intro ref="introRef"></Intro>
    <Introduce ref="introduceRef"></Introduce>
    <Career ref="careerRef"></Career>
    <Project ref="projectRef"></Project>
    <Contact ref="contactRef"></Contact>
  </div>
</template>

<style scoped lang="scss">
div.app-container {
  /* scroll-behavior: smooth; */
  overflow: hidden;
  div.introduce-container,
  div.career-container,
  div.project-container {
    background-color: #2a2a3f;
  }

  div.contact-container {
    background-color: #323248;
  }
}
</style>
