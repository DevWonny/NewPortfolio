<script setup lang="ts"></script>

<template>
  <div class="introduce-container w-screen h-screen flex flex-col justify-between">
    <div class="top-container flex justify-between">
      <div class="self-intro flex flex-col gap-[20px]">
        <div class="picture text-center">Picture</div>
        <div class="short-intro">Short Intro</div>
      </div>

      <div class="self-history">History</div>
    </div>

    <div class="bot-container">Skills</div>
  </div>
</template>

<style scoped lang="scss">
div.introduce-container {
  div.top-container {
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
      background-color: gray;
      width: 50%;
    }
  }
  div.bot-container {
    width: 100%;
    height: 150px;
    background-color: gray;
  }
}
</style>
