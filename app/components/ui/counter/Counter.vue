<script setup lang="ts">
const { base = 10, numberOfDigits = 4 } = defineProps<{
  base?: 2 | 8 | 10 | 16;
  numberOfDigits?: number;
}>();

const modelValue = defineModel<number>({
  default: 0,
});

const base2 = ["0", "1"];
const base8 = ["0", "1", "2", "3", "4", "5", "6", "7"];
const base10 = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
const base16 = [
  "0",
  "1",
  "2",
  "3",
  "4",
  "5",
  "6",
  "7",
  "8",
  "9",
  "A",
  "B",
  "C",
  "D",
  "E",
  "F",
];

const digits = computed(() => {
  switch (base) {
    case 2:
      return base2;
    case 8:
      return base8;
    case 10:
      return base10;
    case 16:
      return base16;
  }
});

const digitsValue = computed(() => {
  const value = modelValue.value.toString(base);

  return value.padStart(numberOfDigits, "0").split("");
});

const previous = usePrevious(modelValue);

const isIncrementing = computed(() => {
  if (previous.value === undefined) return false;

  return modelValue.value > previous.value;
});
</script>

<template>
  <div class="flex items-center rounded bg-neutral-800 p-1">
    <CounterDigit
      v-for="digit in digitsValue"
      :digit="digit"
      :digits="digits"
      :isIncrementing="isIncrementing"
    />
  </div>
  <div class="mt-2 flex items-center gap-2">
    <Button @click="modelValue--">Decrement</Button>
    <Button @click="modelValue++">Increment</Button>
  </div>
</template>
