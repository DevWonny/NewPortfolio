<template>
  <div class="project-card-container" :class="!isOpen && img && 'cursor-pointer effect'">
    <motion.div
      class="motion-container flex items-center justify-center w-[200px] h-[300px]"
      :layout="true"
      :data-open="isOpen"
      @click="toggleOpen()"
    >
      <!-- * Open 전 표출 -->
      <img v-if="!isOpen && img" :src="`/${img}`" alt="Thumbnail" />

      <!-- * Open 했을 경우 표출 -->
      <div v-if="isOpen" class="main">
        <!-- * 회사 프로젝트 - 좌측 이미지 / 우측 경력 기술서 -->
        <!-- * 개인 프로젝트 - 좌측 이미지 / 우측 설명 및 Git Url -->
        <img v-if="mainImg" :src="`/${mainImg}`" alt="Main Image" />
      </div>
    </motion.div>
    <!-- * 해당 div가 열였을때 하단 배열이 깨지지 않도록 하기 위한 div -->
    <div v-if="isOpen" class="empty relative w-[200px] h-[300px]"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { motion } from 'motion-v'

interface Props {
  img?: string
  mainImg?: string
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
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  &.effect {
    &:hover {
      animation-name: shake;
      animation-duration: 0.2s;
      animation-iteration-count: infinite;
    }
  }

  div.motion-container {
    color: #fff;
    z-index: 1;
    &[data-open='true'] {
      width: 1000px;
      height: 600px;
      position: absolute;
      top: calc(50% - 300px);
      left: calc(50% - 500px);
      background-color: #2a2a3f;
    }

    div.main {
      img {
        width: 40%;
        object-fit: cover;
      }
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
