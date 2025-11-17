<template>
  <div class="project-container w-screen h-screen relative flex flex-col">
    <div v-if="overlay" class="overlay absolute w-screen h-screen"></div>
    <div class="company-project flex w-full h-auto">
      <ProjectCard
        :img="'company_1.png'"
        :mainImg="'company_1.png'"
        :projectId="0"
        @stateCheck="onOverlay"
      ></ProjectCard>
      <ProjectCard
        :img="`company_2.png`"
        :mainImg="`company_2_main.png`"
        :projectId="1"
        @stateCheck="onOverlay"
      ></ProjectCard>
    </div>

    <div class="personal-project flex w-full h-auto justify-end">
      <ProjectCard :img="`bookmarker.png`" :projectId="2" @stateCheck="onOverlay"></ProjectCard>
      <ProjectCard :img="`shopmarker.png`" :projectId="3" @stateCheck="onOverlay"></ProjectCard>
      <ProjectCard
        :img="`stock_dashboard.png`"
        :projectId="4"
        @stateCheck="onOverlay"
      ></ProjectCard>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
// component
import ProjectCard from '@/components/ProjectCard.vue'
const overlay = ref(false)
const $emit = defineEmits(['projectOverlay'])

const onOverlay = (check: boolean) => {
  overlay.value = check
  $emit('projectOverlay', check)
}
</script>

<style scoped lang="scss">
div.project-container {
  overflow: hidden;
  gap: 10px;
  div.overlay {
    background-color: rgba(0, 0, 0, 0.7);
    top: 0;
    left: 0;
  }
  div.company-project,
  div.personal-project {
    gap: 30px;
  }
}
</style>
