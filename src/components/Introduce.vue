<template>
  <div class="introduce-container w-screen h-screen flex justify-between">
    <div class="self-intro flex flex-col items-center gap-[50px] w-1/3">
      <div class="picture text-center overflow-hidden relative flex justify-center items-center">
        <img :src="profile" alt="Profile" />
      </div>
      <div class="short-intro overflow-hidden">
        {{
          `안녕하세요.\n3년차 프론트앤드 개발자 윤철원입니다.\nReact, Vue 등 다양한 프레임워크를 다루어 보았으며,\n협업을 중요하게 생각하는 개발자 입니다.`
        }}
      </div>
    </div>

    <div class="self-history flex flex-col w-1/3">
      <!-- * Profile -->
      <div class="profile-container">
        <h2 class="profile"><CircleUserRound />PROFILE</h2>
        <p class="flex flex-row">윤철원</p>
        <p class="flex flex-row gap-[5px]"><Cake /> 1994.02.16</p>
        <p class="flex flex-row gap-[5px]"><MapPinHouse />서울시 관악구</p>
        <p class="flex flex-row gap-[5px]"><FolderCode />Frontend Developer</p>
      </div>

      <!-- * Education -->
      <div class="education-container">
        <h2 class="education"><School />EDUCATION</h2>
        <p>2009.03 ~ 2012.02 | 부산고등학교</p>
        <p>2012.03 ~ 2019.02 | 동명대학교</p>
        <p>2020.10 ~ 2021.05 | SBS 아카데미 컴퓨터 아트 학원</p>
      </div>

      <!-- * Certification -->
      <div class="certification-container">
        <h2 class="certification"><Award />CERTIFICATION</h2>
        <!-- * 년월 | 이름 -->
        <p>2021.04 | 웹디자인 기능사</p>
        <p>2021.06 | 정보처리기사</p>
      </div>

      <!-- * Career -->
      <div class="career-container">
        <h2 class="career"><BriefcaseBusiness />CAREER</h2>
        <!-- * 입사년도월일 ~ 퇴사년도월일 | 이름 -->
        <p>2022.02 ~ 2022.08 | 프래프</p>
        <p>2022.11 ~ 2025.01 | 비투지게임즈</p>
      </div>
    </div>

    <div class="skill-container h-fit flex flex-wrap justify-start w-1/3">
      <div
        v-for="(icon, i) in iconArray"
        :key="`skill-item-${icon}-${i}`"
        class="w-1/4 h-[100px] flex justify-center items-center flex-col gap-[10px]"
      >
        <Icon :icon="`simple-icons:${icon}`" width="32" height="32" />
        <p class="text-xs w-full text-center">{{ onConvertName(icon) }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import {
  Cake,
  MapPinHouse,
  FolderCode,
  School,
  CircleUserRound,
  Award,
  BriefcaseBusiness,
} from 'lucide-vue-next'
import { Icon } from '@iconify/vue'
// image
import profile from '@/assets/profile.jpg'

const iconArray = ref([
  'html5',
  'css3',
  'sass',
  'tailwindcss',
  'javascript',
  'typescript',
  'react',
  'vuedotjs',
  'nextdotjs',
  'nuxt',
])

const onConvertName = (name: string) => {
  switch (name) {
    case 'html5':
      return 'HTML'

    case 'css3':
      return 'CSS'

    case 'sass':
      return 'SCSS'

    case 'tailwindcss':
      return 'Tailwind'

    case 'javascript':
      return 'Javascript'

    case 'typescript':
      return 'Typescript'

    case 'react':
      return 'React'

    case 'vuedotjs':
      return 'Vue'

    case 'nextdotjs':
      return 'Next.js'

    case 'nuxt':
      return 'Nuxt.js'
  }
}
</script>

<style scoped lang="scss">
div.introduce-container {
  div.self-intro {
    div.picture {
      border-radius: 50%;
      background-color: white;
      width: 200px;
      height: 200px;
      color: #000;
    }
    div.short-intro {
      white-space: pre;
    }
  }

  div.self-history {
    gap: 20px;
    padding: 0 20px;
    border-right: 0.5px solid rgba(154, 154, 154, 0.5);
    border-left: 0.5px solid rgba(154, 154, 154, 0.5);
    div {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    h2 {
      display: flex;
      flex-direction: row;
      align-items: center;
      text-decoration: underline;
      text-underline-offset: 5px;
      font-size: 18px;
      gap: 10px;
    }
  }
}
</style>
