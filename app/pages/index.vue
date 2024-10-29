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

// Create an array of numbers 0-9 for the rolling effect
const digits = Array.from({ length: 10 }, (_, i) => i);

// Helper function to parse digit string to number
const getDigitValue = (digit: string) => parseInt(digit, 10);
</script>

<template>
  <div class="relative mx-auto max-w-5xl px-4">
    <div
      class="absolute inset-0 bg-[radial-gradient(theme(colors.border/90%)_1px,transparent_1px)] [background-size:20px_20px] [mask-image:radial-gradient(ellipse_50%_50%_at_50%_50%,#000_50%,transparent_100%)]"
    />
    <div
      class="relative z-10 flex flex-col items-center justify-center gap-6 py-16 text-center lg:py-24"
    >
      <div class="odometer">
        <div
          v-for="(digit, index) in formattedCounter"
          :key="index"
          class="digit-column"
        >
          <div
            class="digits-wrapper"
            :style="{
              transform: `translateY(-${getDigitValue(digit) * 3}rem)`,
            }"
          >
            <div v-for="n in digits" :key="n" class="digit">
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

<style scoped>
.odometer {
  display: flex;
  gap: 2px;
  background: #000;
  padding: 8px;
  border-radius: 8px;
}

.digit-column {
  height: 3rem;
  overflow: hidden;
  background: #222;
  border-radius: 4px;
}

.digits-wrapper {
  transition: transform 0.3s ease-in-out;
}

.digit {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 3rem;
  width: 2rem;
  font-family: "Courier New", Courier, monospace;
  font-size: 2rem;
  color: #fff;
  font-weight: bold;
}
</style>
