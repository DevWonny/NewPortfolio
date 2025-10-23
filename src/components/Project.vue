<template>
  <div class="project-container w-screen h-screen relative flex flex-col">
    <div class="company-project flex w-full h-auto">
      <ProjectCard :check="'company1'"></ProjectCard>
      <ProjectCard :check="'company2'"></ProjectCard>
    </div>

    <div class="personal-project flex w-full h-auto justify-end">
      <ProjectCard :check="'personal1'"></ProjectCard>
      <ProjectCard :check="'personal2'"></ProjectCard>
      <ProjectCard :check="'personal3'"></ProjectCard>
    </div>
  </div>
</template>

<script setup lang="ts">
// component
import ProjectCard from '@/components/ProjectCard.vue'
</script>

<style scoped lang="scss">
div.project-container {
  overflow: hidden;
  gap: 10px;
  div.company-project,
  div.personal-project {
    gap: 30px;
  }
}
</style>
