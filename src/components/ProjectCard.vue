<template>
  <div class="project-card-container" :class="!isOpen && 'cursor-pointer'">
    <motion.div
      class="motion-container flex items-center justify-center w-[200px] h-[300px]"
      :layout="true"
      :data-open="isOpen"
      @click="toggleOpen()"
    >
      <p>{{ check }}</p>
      <a v-if="isOpen" href="https://www.naver.com" target="_blank">test</a>
    </motion.div>
    <div v-if="isOpen" class="empty relative w-[200px] h-[300px]"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { motion } from 'motion-v'

interface Props {
  check: string
}

// props
const props = defineProps<Props>()
const $emit = defineEmits(['stateCheck'])
const isOpen = ref(false)

const toggleOpen = () => {
  isOpen.value = !isOpen.value
  $emit('stateCheck', isOpen.value)
}
</script>

<style scoped lang="scss">
div.project-card-container {
  height: 300px;
  &:hover {
    animation-name: shake;
    animation-duration: 0.2s;
    animation-iteration-count: infinite;
  }

  div.motion-container {
    background-color: #fff;
    color: black;
    z-index: 1;
    &[data-open='true'] {
      width: 400px;
      height: 600px;
      position: absolute;
      top: calc(50% - 300px);
      left: calc(50% - 200px);
    }
  }
}

@keyframes shake {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(2deg);
  }
  75% {
    transform: rotate(-2deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
</style>
