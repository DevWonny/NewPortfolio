<template>
  <div class="project-container w-screen h-screen relative flex flex-col">
    <div v-if="overlay" class="overlay absolute w-screen h-screen"></div>
    <div class="company-project flex w-full h-auto">
      <ProjectCard
        :img="'company1'"
        :mainImg="'company1'"
        :projectId="0"
        @stateCheck="onOverlay"
      ></ProjectCard>
      <ProjectCard
        :img="`company2`"
        :mainImg="`company2Main`"
        :projectId="1"
        @stateCheck="onOverlay"
      ></ProjectCard>
    </div>

    <div class="personal-project flex w-full h-auto justify-end">
      <ProjectCard :img="`bookmarker`" :projectId="2" @stateCheck="onOverlay"></ProjectCard>
      <ProjectCard :img="`stockDashboard`" :projectId="3" @stateCheck="onOverlay"></ProjectCard>
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
