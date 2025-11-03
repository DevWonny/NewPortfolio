<template>
  <div class="project-card-container">
    <motion.div
      class="motion-container flex items-center justify-center w-[200px] h-[300px]"
      :layout="true"
      :data-open="isOpen"
      @click="toggleOpen()"
    >
      <p>{{ check }}</p>
    </motion.div>
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
  div.motion-container {
    background-color: #fff;
    color: black;
    &[data-open='true'] {
      width: 400px;
      height: 600px;
      position: absolute;
      top: calc(50% - 300px);
      left: calc(50% - 200px);
    }
  }
}
</style>
