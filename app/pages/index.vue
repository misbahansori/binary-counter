<script setup lang="ts">
import { computed, ref } from "vue";

const counter = ref(0);

const increment = () => {
  counter.value++;
};

const decrement = () => {
  counter.value--;
};

// Format the counter value as a string with leading zeros
const formattedCounter = computed(() => {
  return counter.value.toString().padStart(3, "0");
});

// Modified: Add an extra 0 at the end for smooth transition from 9 to 0
const digits = [...Array.from({ length: 10 }, (_, i) => i), 0];

// Modified: Calculate position considering the extra digit
const getDigitTransform = (digit: string) => {
  const value = parseInt(digit, 10);
  return `translateY(-${value * 3}rem)`;
};
</script>

<template>
  <div class="relative mx-auto max-w-5xl px-4">
    <div
      class="absolute inset-0 bg-[radial-gradient(theme(colors.border/90%)_1px,transparent_1px)] [background-size:20px_20px] [mask-image:radial-gradient(ellipse_50%_50%_at_50%_50%,#000_50%,transparent_100%)]"
    />
    <div
      class="relative z-10 flex flex-col items-center justify-center gap-6 py-16 text-center lg:py-24"
    >
      <div class="flex gap-0.5 rounded-lg bg-black p-2">
        <div
          v-for="(digit, index) in formattedCounter"
          :key="index"
          class="h-12 overflow-hidden rounded bg-neutral-800"
        >
          <div
            class="transition-transform duration-300 ease-in-out"
            :style="{
              transform: getDigitTransform(digit),
            }"
          >
            <div
              v-for="n in digits"
              :key="n"
              class="flex h-12 w-8 items-center justify-center font-orbitron text-2xl font-bold text-white"
            >
              {{ n }}
            </div>
          </div>
        </div>
      </div>

      <div class="flex items-center gap-3">
        <Button @click="increment">Increment</Button>
        <Button @click="decrement">Decrement</Button>
      </div>
    </div>
  </div>
</template>
