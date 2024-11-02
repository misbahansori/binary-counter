<script setup lang="ts">
import { ref } from "vue";

const decimalNumber = ref(0);
</script>

<template>
  <div class="relative mx-auto max-w-5xl px-4">
    <div
      class="absolute inset-0 bg-[radial-gradient(theme(colors.border/90%)_1px,transparent_1px)] [background-size:20px_20px] [mask-image:radial-gradient(ellipse_50%_50%_at_50%_50%,#000_50%,transparent_100%)]"
    />
    <div
      class="relative z-10 flex flex-col items-center justify-center gap-12 py-16 text-center lg:py-24"
    >
      <div class="flex flex-col items-center gap-6">
        <Counter v-model="decimalNumber" />
      </div>
    </div>
  </div>
</template>
