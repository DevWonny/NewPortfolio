<template>
  <div class="introduce-container w-screen h-screen flex justify-between">
    <div class="self-intro flex flex-col gap-[50px]">
      <div class="picture text-center">Picture</div>
      <div class="short-intro">Short Intro</div>
    </div>

    <div class="self-history flex flex-col">
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

    <div class="skill-container"></div>
  </div>
</template>

<script setup lang="ts">
import {
  Cake,
  MapPinHouse,
  FolderCode,
  School,
  CircleUserRound,
  Award,
  BriefcaseBusiness,
} from 'lucide-vue-next'
</script>

<style scoped lang="scss">
div.introduce-container {
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

  div.skill-container {
    background-color: gray;
    width: 30%;
    height: 100px;
  }
}
</style>
