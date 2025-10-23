<template>
  <div class="project-container w-screen h-screen relative">
    <ProjectCard></ProjectCard>
    <ProjectCard></ProjectCard>
    <ProjectCard></ProjectCard>
    <ProjectCard></ProjectCard>
    <ProjectCard></ProjectCard>
  </div>
</template>

<script setup lang="ts">
// component
import ProjectCard from '@/components/ProjectCard.vue'
</script>

<style scoped lang="scss">
div.project-container {
  overflow: hidden;
}
</style>
