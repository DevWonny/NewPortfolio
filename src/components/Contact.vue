<script setup lang="ts">
// throttle(() => {
//   console.log(111)
//   if (isScrolling) return
//   isScrolling = true

//   if (event.deltaY > 0 && currentIndex.value < sections.value.length - 1) {
//     currentIndex.value++
//   } else if (event.deltaY < 0 && currentIndex.value > 0) {
//     currentIndex.value--
//   }

//   sections.value[currentIndex.value]?.scrollIntoView({ behavior: 'smooth' })

//   setTimeout(() => {
//     isScrolling = false
//   }, 800)
// }, 100)
</script>

<template>
  <div class="contact-container w-screen h-screen">Contact</div>
</template>

<style scoped lang="scss"></style>
