<template>
  <div class="contact-container w-screen h-screen flex flex-col items-center justify-center">
    <!-- ! 어떤 문구 넣을지 생각하기... & Framer Motion 활용 하기 -->
    <h1 class="contact-message text-8xl">TITLE</h1>

    <div class="icon-container flex items-center justify-between">
      <div :over="isMailOver">
        <Mail
          class="cursor-pointer"
          @mouseover="isMailOver = true"
          @mouseleave="isMailOver = false"
          @click="clipboard"
          :size="50"
        />
      </div>

      <div :over="isGithubOver">
        <a href="https://github.com/DevWonny" target="_blank" rel="noopener noreferrer">
          <Github
            class="cursor-pointer"
            @mouseover="isGithubOver = true"
            @mouseleave="isGithubOver = false"
            :size="50"
          />
        </a>
      </div>

      <div :over="isResumeOver">
        <FileUser
          class="cursor-pointer"
          @mouseover="isResumeOver = true"
          @mouseleave="isResumeOver = false"
          :size="50"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Mail, Github, FileUser } from 'lucide-vue-next'
import { ref } from 'vue'

const isMailOver = ref(false)
const isGithubOver = ref(false)
const isResumeOver = ref(false)

const clipboard = () => {
  navigator.clipboard.writeText('cjfdnjs1994@naver.com')
  alert('이메일이 클립보드에 저장되었습니다.')
}
</script>

<style scoped lang="scss">
div.contact-container {
  gap: 80px;

  div.icon-container {
    gap: 100px;
    div {
      color: #9a9a9a;
      transition-duration: 0.2s;
      &[over='true'] {
        transform: scale(2);
        color: #fff;
      }
    }
  }
}
</style>
