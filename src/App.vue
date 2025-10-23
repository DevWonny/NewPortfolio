<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import { throttle } from 'lodash'
// component
import Intro from '@/components/Intro.vue'
import Introduce from '@/components/Introduce.vue'
import Project from '@/components/Project.vue'
import Contact from '@/components/Contact.vue'

const introRef = ref()
const introduceRef = ref()
const projectRef = ref()
const contactRef = ref()

const sections = ref<HTMLElement[]>([])
const currentIndex = ref(0)
let isScrolling = false

// Wheel Event
const onWheel = (e: WheelEvent) => {
  e.preventDefault()

  if (isScrolling) return
  isScrolling = true
  if (e.deltaY > 0 && currentIndex.value < sections.value.length - 1) {
    currentIndex.value++
  } else if (e.deltaY < 0 && currentIndex.value > 0) {
    currentIndex.value--
  }

  sections.value[currentIndex.value]?.scrollIntoView({ behavior: 'smooth' })
  setTimeout(() => {
    isScrolling = false
  }, 800)
}

onMounted(async () => {
  await nextTick()

  sections.value = [
    introRef.value?.$el,
    introduceRef.value?.$el,
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
    <Project ref="projectRef"></Project>
    <Contact ref="contactRef"></Contact>
  </div>
</template>

<style scoped lang="scss">
div.app-container {
  overflow-x: hidden;
  div.introduce-container,
  div.project-container {
    background-color: #2a2a3f;
    padding: 50px 100px;
  }

  div.contact-container {
    background-color: #323248;
  }
}
</style>
