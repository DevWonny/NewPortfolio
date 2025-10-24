<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import { Mouse, CircleArrowUp } from 'lucide-vue-next'
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

const onScrollToTop = () => {
  if (currentIndex.value !== 3) return

  if (isScrolling) return
  currentIndex.value = 0
  isScrolling = true
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

    <Mouse class="mouse-icon fixed" v-show="currentIndex !== 3" />
    <CircleArrowUp
      class="top-button fixed cursor-pointer"
      v-show="currentIndex === 3"
      @click="onScrollToTop"
    />
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

  .mouse-icon {
    bottom: 0;
    left: 0;
  }

  .top-button {
    bottom: 0;
    right: 0;
  }
}
</style>
