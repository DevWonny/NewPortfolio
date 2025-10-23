<template>
  <div class="project-card-container">
    <motion.div
      class="motion-container flex items-center justify-center w-[200px] h-[300px]"
      :layout="true"
      :data-open="isOpen"
      @click="toggleOpen"
    >
      <!-- <motion.div class="motion-content" :data-open="isOpen" :layout="true"></motion.div> -->
    </motion.div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { motion } from 'motion-v'

const isOpen = ref(false)
const toggleOpen = () => {
  isOpen.value = !isOpen.value
}
</script>

<style scoped lang="scss">
div.project-card-container {
  margin-bottom: 10px;
  div.motion-container {
    background-color: #fff;
    &[data-open='true'] {
      width: 400px;
      height: 600px;
      position: relative;
      top: 50%;
      left: 50%;
    }
  }
}
</style>
