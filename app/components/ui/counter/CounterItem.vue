<script setup lang="ts">
interface Props {
  value: string;
  base: 2 | 8 | 10 | 16;
}

const props = defineProps<Props>();

// Generate digits based on the base
const digits = computed(() => {
  switch (props.base) {
    case 2:
      return ["0", "1"];
    case 8:
      return ["0", "1", "2", "3", "4", "5", "6", "7"];
    case 16:
      return [
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
    default:
      return ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
  }
});

// Calculate the position based on the current value
const position = computed(() => {
  return digits.value.indexOf(props.value.toUpperCase()) * 3;
});
</script>

<template>
  <div class="h-12 overflow-hidden rounded bg-neutral-800">
    <div
      class="transition-transform duration-300 ease-in-out"
      :style="{
        transform: `translateY(-${position}rem)`,
      }"
    >
      <div
        v-for="n in digits"
        :key="n"
        class="flex h-12 w-8 items-center justify-center font-orbitron text-3xl font-bold text-white"
      >
        {{ n }}
      </div>
    </div>
  </div>
</template>
