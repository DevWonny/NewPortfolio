<template>
  <div class="contact-container w-screen h-screen">
    <Mail />
    <Github />
    <FileUser :size="80" :stroke-width="1" />
  </div>
</template>

<script setup lang="ts">
import { Mail, Github, FileUser } from 'lucide-vue-next'
</script>

<style scoped lang="scss"></style>
