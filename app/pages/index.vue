<script setup lang="ts">
import { ref } from "vue";

const binaryValue = ref(0);
const octalValue = ref(0);
const decimalValue = ref(0);
const hexValue = ref(0);
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
        <Counter :value="binaryValue" :digits="8" :base="2" />
        <div class="flex items-center gap-3">
          <Button @click="binaryValue++">Increment</Button>
          <Button @click="binaryValue--">Decrement</Button>
        </div>
      </div>

      <div class="flex flex-col items-center gap-6">
        <Counter :value="octalValue" :digits="6" :base="8" />
        <div class="flex items-center gap-3">
          <Button @click="octalValue++">Increment</Button>
          <Button @click="octalValue--">Decrement</Button>
        </div>
      </div>

      <div class="flex flex-col items-center gap-6">
        <Counter :value="decimalValue" :digits="4" :base="10" />
        <div class="flex items-center gap-3">
          <Button @click="decimalValue++">Increment</Button>
          <Button @click="decimalValue--">Decrement</Button>
        </div>
      </div>

      <div class="flex flex-col items-center gap-6">
        <Counter :value="hexValue" :digits="4" :base="16" />
        <div class="flex items-center gap-3">
          <Button @click="hexValue++">Increment</Button>
          <Button @click="hexValue--">Decrement</Button>
        </div>
      </div>
    </div>
  </div>
</template>
