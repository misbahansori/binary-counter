<script setup lang="ts">
import { computed } from "vue";

interface Props {
  value: number;
  digits: number;
  base?: 2 | 8 | 10 | 16;
}

const props = withDefaults(defineProps<Props>(), {
  base: 10,
});

// Format the counter value based on the selected base
const formattedCounter = computed(() => {
  let formatted = "";
  switch (props.base) {
    case 2:
      formatted = props.value.toString(2);
      break;
    case 8:
      formatted = props.value.toString(8);
      break;
    case 16:
      formatted = props.value.toString(16).toUpperCase();
      break;
    default:
      formatted = props.value.toString();
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
  </div>
</template>
