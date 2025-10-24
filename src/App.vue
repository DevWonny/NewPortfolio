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

    <div
      class="mouse-icon-container fixed flex flex-col items-center justify-center gap-[10px] cursor-default"
      v-show="currentIndex === 0"
    >
      <Mouse class="icon relative" :size="50" />
      <span>SCROLL!</span>
    </div>

    <CircleArrowUp
      class="top-button fixed cursor-pointer"
      v-show="currentIndex === 3"
      @click="onScrollToTop"
      :size="50"
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

  div.mouse-icon-container {
    bottom: 50px;
    left: 50%;
    transform: translateX(-50%);

    .icon {
      animation-duration: 1s;
      animation-name: updown;
      animation-iteration-count: infinite;
    }
  }

  .top-button {
    bottom: 50px;
    right: 100px;
    color: #9a9a9a;
    transition-duration: 0.2s;
    &:hover {
      color: #fff;
    }
  }
}

@keyframes updown {
  0% {
    top: 0px;
  }
  50% {
    top: 10px;
  }
  100% {
    top: 0px;
  }
}
</style>
