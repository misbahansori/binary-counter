<script setup lang="ts">
import { computed, ref } from "vue";

interface Props {
  digits: number;
  base?: 2 | 8 | 10 | 16; // Allow binary, octal, decimal, and hexadecimal
}

const props = withDefaults(defineProps<Props>(), {
  base: 10,
});

const counter = ref(0);

const increment = () => {
  counter.value++;
};

const decrement = () => {
  counter.value--;
};

// Format the counter value based on the selected base
const formattedCounter = computed(() => {
  let formatted = "";
  switch (props.base) {
    case 2:
      formatted = counter.value.toString(2);
      break;
    case 8:
      formatted = counter.value.toString(8);
      break;
    case 16:
      formatted = counter.value.toString(16).toUpperCase();
      break;
    default:
      formatted = counter.value.toString();
  }
  return formatted.padStart(props.digits, "0");
});
</script>

<template>
  <div class="flex flex-col items-center justify-center gap-6">
    <div class="flex items-center gap-4">
      <span class="text-sm font-medium text-muted-foreground">
        Base-{{ base }}
      </span>
      <div class="flex gap-0.5 rounded-lg bg-black p-2">
        <CounterItem
          v-for="(digit, index) in formattedCounter"
          :key="index"
          :value="digit"
          :base="base"
        />
      </div>
    </div>

    <div class="flex items-center gap-3">
      <Button @click="increment">Increment</Button>
      <Button @click="decrement">Decrement</Button>
    </div>
  </div>
</template>
