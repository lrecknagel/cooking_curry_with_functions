<script setup lang="ts">
import { computed } from 'vue'
import { handleBackground } from '../layoutHelper'
const props = defineProps({
  imageLeft: {
    type: String,
  },
  imageRight: {
    type: String,
  },
})
const left = computed(() => handleBackground(props.imageLeft))
const right = computed(() => handleBackground(props.imageRight))
</script>

<template>
  <div class="grid grid-cols-2 w-full h-full gap-x-7">
    <slot />
    <div class="ml-14 my-20" :style="left"></div>
    <!-- <div class="grid w-full h-full"> -->
      <div class="ml-14 my-30" :style="right"></div>
    <!-- </div> -->
  </div>
</template>
