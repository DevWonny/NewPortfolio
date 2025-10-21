<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
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
let isScrolling = false

// Scroll Event
const onScrollEvent = (event: WheelEvent) => {
  event.preventDefault()

  if (isScrolling) return
  isScrolling = true
  console.log('🚀 ~ onScrollEvent ~ currentIndex.value:', currentIndex.value)
  console.log('🚀 ~ onScrollEvent ~ sections.value.length - 1:', sections.value.length - 1)
  if (event.deltaY > 0 && currentIndex.value < sections.value.length - 1) {
    currentIndex.value++
  } else if (event.deltaY < 0 && currentIndex.value > 0) {
    currentIndex.value--
  }

  sections.value[currentIndex.value]?.scrollIntoView({ behavior: 'smooth' })

  setTimeout(() => {
    isScrolling = false
  }, 800) // 스크롤 중복 방지
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

  window.addEventListener('wheel', onScrollEvent, { passive: false })
})

onBeforeUnmount(() => {
  window.removeEventListener('wheel', onScrollEvent)
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
