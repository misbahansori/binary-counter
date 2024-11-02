<script setup lang="ts">
const { digits = 4 } = defineProps<{
  digits?: number;
}>();

const modelValue = defineModel<number>({
  default: 0,
});

const digitsValue = computed(() => {
  return modelValue.value.toString().padStart(digits, "0").split("");
});

const base10 = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
</script>

<template>
  <div class="flex items-center rounded bg-neutral-800 p-1">
    <CounterDigit
      v-for="digit in digitsValue"
      :digit="digit"
      :digits="base10"
    />
  </div>
  <div class="mt-2 flex items-center gap-2">
    <Button @click="modelValue--">Decrement</Button>
    <Button @click="modelValue++">Increment</Button>
  </div>
</template>
