<template>
  <div class="project-card-container" :class="!isOpen && img && 'cursor-pointer effect'">
    <motion.div
      class="motion-container flex items-center justify-center w-[200px] h-[300px]"
      :layout="true"
      :data-open="isOpen"
      @click="toggleOpen()"
    >
      <button v-if="isOpen" class="close-btn absolute cursor-pointer" @click.stop="modalClose">
        <X />
      </button>
      <!-- * Open 전 표출 -->
      <img v-if="!isOpen && img" :src="`/${img}`" alt="Thumbnail" />

      <!-- * Open 했을 경우 표출 -->
      <div v-if="isOpen" class="main flex justify-between">
        <!-- * 회사 프로젝트 - 좌측 이미지 / 우측 경력 기술서 -->
        <!-- * 개인 프로젝트 - 좌측 이미지 / 우측 설명 및 Git Url -->
        <img v-if="mainImg" :src="`/${mainImg}`" alt="Main Image" />
        <img v-if="!mainImg" :src="`/${img}`" alt="Image" />
        <div class="description-container">
          <!-- * 프로젝트 명칭 / 사용 기술 스텍 / 기간 / 투입 인원 / 역할 / 간략 경력 기술 -->
          <!-- * 개인 플젝일 경우 -> 간략 경력 기술 대신 해당 플젝을 만든 계기 입력 + Github Link + 프로젝트 사이트 Link -->
          <div class="description" v-if="projectId === 0">
            <p>프로젝트 명 : 오토앤 공임비교 앱</p>
            <p>연계 및 소속 회사 : 오토앤 / 프래프</p>
            <p>주요 업무 : 프론트엔드 개발 업무</p>
            <p>
              {{
                `담당 업무 : Validation 작업 / 회원가입 작업 /\n차량 등록 및 수정 페이지 작업 / 예약페이지 작업 / 마이페이지 작업`
              }}
            </p>
            <p>기술 스택 : Javascript / React</p>
            <p>개발 기간 : 2022.05 ~ 2022. 08</p>
            <p>투입 인원 : 7명 (디자이너 1명, 퍼블리셔 1명, 프론트엔드 3명, 백엔드 1명)</p>
          </div>

          <div class="description" v-if="projectId === 1">
            <p>프로젝트 명 : FanFan(가칭)</p>
            <p>소속 회사 : 비투지게임즈</p>
            <p>주요 업무 : 프론트엔드 개발 업무</p>
            <p>
              {{
                `담당 업무 : 메인 페이지 / 마이페이지 / 판타지 게임(라이브) 페이지 \n/ 시뮬레이션 페이지 / 플레이트 마켓(카드 구입) 페이지 / 스카우트(카드 강화) 페이지 \n/ 샵 페이지(퍼블리싱) / 랭킹 페이지`
              }}
            </p>
            <p>기술 스택 : Typescript / Vue / Nuxt.js / Pinia / SCSS / Jira / Notion / Postman</p>
            <p>개발 기간 : 2022.12 ~ 2025.01</p>
            <p>투입 인원 : 12명 ~ 15명 (프로젝트 진행 중 인력 교체로 인한 인원변동 발생)</p>
          </div>

          <div class="description" v-if="projectId === 2">
            <p>프로젝트 명 : Bookmarker</p>
            <p>소개 : 당시 책 읽는 빈도가 많아져 생각하게 된 아이디어로 만든 개인 프로젝트.</p>
            <p>기술 스택 : Typescript / Next.js / SCSS / TailwindCSS / Zustand</p>
            <p>개발 기간 : 2025.04 ~ 2025.06</p>
            <a href="https://bookmarker-liard.vercel.app/" target="_blank">바로가기</a>
          </div>

          <div class="description" v-if="projectId === 3">
            <p>프로젝트 명 : Shopmarker</p>
            <p>소개 : 카드사 연결을 경험해보지 못해서 경험을 해보기 위해 만든 개인 프로젝트.</p>
            <p>
              기술 스택 : Typescript / Next.js / SCSS / TailwindCSS / Zustand /토스 페이먼츠 API /
              Fake Store API / Firebase Auth
            </p>
            <p>개발 기간 : 2025.06 ~ 2025.08</p>
            <!-- * 링크 변경 필요 -->
            <a href="https://bookmarker-liard.vercel.app/" target="_blank">바로가기</a>
          </div>

          <div class="description" v-if="projectId === 4">
            <p>프로젝트 명 : StockDashboard</p>
            <p>
              소개 : 주식 관련 뉴스를 보다 차트 및 실시간 통신에 관한 기능을 경험하고자 시작한 개인
              프로젝트.
            </p>
            <p>
              기술 스택 : Typescript / Next.js / SCSS / TailwindCSS / Socket.io / Express / Finnhub
            </p>
            <p>개발 기간 : 2025.09 ~ 2025.11</p>
            <a href="https://stock-dashboard-ten-rho.vercel.app/" target="_blank">바로가기</a>
          </div>
        </div>
      </div>
    </motion.div>

    <!-- * 해당 div가 열였을때 하단 배열이 깨지지 않도록 하기 위한 div -->
    <div v-if="isOpen" class="empty relative w-[200px] h-[300px]"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { motion } from 'motion-v'
import { X } from 'lucide-vue-next'

interface Props {
  img?: string
  mainImg?: string
  projectId: number
}

// props
const props = defineProps<Props>()
const $emit = defineEmits(['stateCheck'])
const isOpen = ref(false)

const toggleOpen = () => {
  if (isOpen.value) {
    return
  }
  isOpen.value = true
  $emit('stateCheck', isOpen.value)
}

const modalClose = () => {
  isOpen.value = false
  $emit('stateCheck', isOpen.value)
}
</script>

<style scoped lang="scss">
div.project-card-container {
  height: 300px;
  overflow: hidden;
  border-radius: 8px;

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
  button.close-btn {
    top: 20px;
    right: 20px;
    color: #9a9a9a;
    &:hover {
      color: #fff;
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
      padding: 20px 40px;
      img {
        width: 40%;
        object-fit: cover;
      }

      div.description-container {
        /* padding: 10px 20px; */
        div.description {
          display: flex;
          flex-direction: column;
          gap: 10px;
          p {
            white-space: pre-wrap;
          }
        }
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
