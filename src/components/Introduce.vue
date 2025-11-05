<template>
  <div class="introduce-container w-screen h-screen flex flex-col justify-between">
    <div class="top-container flex justify-between">
      <div class="self-intro flex flex-col gap-[20px]">
        <div class="picture text-center">Picture</div>
        <div class="short-intro">Short Intro</div>
      </div>

      <div class="self-history flex flex-col">
        <!-- * Profile -->
        <div class="profile-container">
          <h2 class="profile">PROFILE</h2>
          <!-- * 이름 / 출생년도 / 주소지 / 직무 -->
          <p class="flex flex-row">윤철원</p>
          <p class="flex flex-row gap-[5px]"><Cake /> 1994.02.16</p>
          <p class="flex flex-row gap-[5px]"><MapPinHouse />서울시 관악구</p>
          <p class="flex flex-row gap-[5px]"><FolderCode />Frontend Developer</p>
        </div>

        <!-- * Education -->
        <div class="education-container">
          <h2 class="education">EDUCATION</h2>
          <!-- * 고 / 대 / 학원 -->
          <!-- * 년월 | 명칭 -->
        </div>

        <!-- * Certification -->
        <div class="certification-container">
          <h2 class="certification">CERTIFICATION</h2>
          <!-- * 정보처리기사 -->
          <!-- * 년월 | 이름 -->
        </div>

        <!-- * Career -->
        <div class="career-container">
          <h2 class="career">CAREER</h2>
          <!-- * 입사년도월일 ~ 퇴사년도월일 | 이름 -->
        </div>
      </div>
    </div>

    <div class="bot-container">Skills</div>
  </div>
</template>

<script setup lang="ts">
import { Cake, MapPinHouse, FolderCode } from 'lucide-vue-next'
</script>

<style scoped lang="scss">
div.introduce-container {
  div.top-container {
    div.self-intro {
      div.picture {
        border-radius: 50%;
        background-color: white;
        width: 300px;
        height: 300px;
        color: #000;
      }
      div.short-intro {
        background-color: gray;
        width: 300px;
        height: 100px;
      }
    }

    div.self-history {
      background-color: gray;
      width: 50%;
      gap: 20px;
      div {
        display: flex;
        flex-direction: column;
        gap: 10px;
      }
      h2 {
        text-decoration: underline;
        text-underline-offset: 5px;
        font-size: 18px;
      }
    }
  }
  div.bot-container {
    width: 100%;
    height: 150px;
    background-color: gray;
  }
}
</style>
