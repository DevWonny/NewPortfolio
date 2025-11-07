<template>
  <div class="contact-container w-screen h-screen flex flex-col items-center justify-center">
    <!-- ! 어떤 문구 넣을지 생각하기... & Framer Motion 활용 하기 -->
    <h1 class="contact-message text-8xl">CONTACT ME</h1>

    <div class="icon-container flex items-center justify-between">
      <div class="icon">
        <Mail
          class="cursor-pointer"
          @mouseover="isMailOver = true"
          @mouseleave="isMailOver = false"
          @click="clipboard"
          :size="50"
        />
      </div>

      <div class="icon">
        <a href="https://github.com/DevWonny" target="_blank" rel="noopener noreferrer">
          <Github
            class="cursor-pointer"
            @mouseover="isGithubOver = true"
            @mouseleave="isGithubOver = false"
            :size="50"
          />
        </a>
      </div>

      <div class="icon">
        <a href="/resume.pdf" download="윤철원_이력서.pdf">
          <FileUser
            class="cursor-pointer"
            @mouseover="isResumeOver = true"
            @mouseleave="isResumeOver = false"
            :size="50"
          />
        </a>
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
    div.icon {
      color: #9a9a9a;
      transition-duration: 0.2s;
      &:hover {
        color: #fff;
        transform: scale(2);
      }
    }
  }
}
</style>
