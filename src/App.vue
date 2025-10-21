<script setup lang="ts">
import { ref, onMounted, computed, onUpdated } from 'vue'
// component
import Intro from '@/components/Intro.vue'
import Introduce from '@/components/Introduce.vue'
import Career from '@/components/Career.vue'
import Project from '@/components/Project.vue'
import Contact from '@/components/Contact.vue'

const introRef = ref()
const introduceRef = ref()
const careerRef = ref()
const projectRef = ref()
const contactRef = ref()
</script>

<template>
  <div class="app-container">
    <Intro></Intro>
    <Introduce></Introduce>
    <!-- <Career></Career> -->
    <!-- <Project></Project> -->
    <!-- <Contact></Contact> -->
  </div>
</template>

<style scoped lang="scss">
div.app-container {
  div.introduce-container,
  div.career-container,
  div.project-container {
    background-color: #2a2a3f;
  }

  div.contact-container {
    background-color: #323248;
  }
}
</style>
