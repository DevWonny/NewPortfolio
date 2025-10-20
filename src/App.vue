<script setup lang="ts">
// component
import Intro from '@/components/Intro.vue'
import Introduce from '@/components/Introduce.vue'
import Career from '@/components/Career.vue'
import Project from '@/components/Project.vue'
import Contact from '@/components/Contact.vue'
</script>

<template>
  <div>
    <Intro></Intro>
    <Introduce></Introduce>
    <Career></Career>
    <Project></Project>
    <Contact></Contact>
  </div>
</template>

<style scoped lang="scss">
div.intro-container {
  background-color: #0b0c2a;
}

div.introduce-container,
div.career-container,
div.project-container {
  background-color: #2a2a3f;
}

div.contact-container {
  background-color: #323248;
}
</style>
