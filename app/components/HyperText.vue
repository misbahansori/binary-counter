<template>
  <div
    class="flex scale-100 cursor-default overflow-hidden py-2"
    @mouseenter="triggerAnimation"
  >
    <div class="flex">
      <span
        v-for="(letter, i) in displayText"
        :key="i"
        :class="cn(letter === ' ' ? 'w-3' : '', $props.class)"
        class="inline-block font-mono"
        v-motion
        :initial="{ opacity: 0, y: -10 }"
        :enter="{ opacity: 1, y: 0 }"
        :delay="i * (duration / (text.length * 10))"
      >
        {{ letter.toUpperCase() }}
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useIntervalFn } from "@vueuse/core";
import { computed, ref, watch } from "vue";

const props = defineProps<{
  text: string;
  duration: number;
  class?: string;
  animateOnLoad?: boolean;
}>();

const alphabets = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const displayText = ref<string[]>(props.text.split(""));
const iterations = ref(0);
const getRandomLetter = () =>
  alphabets[Math.floor(Math.random() * alphabets.length)];

const triggerAnimation = () => {
  iterations.value = 0;
  startAnimation();
};

const { pause, resume } = useIntervalFn(
  () => {
    if (iterations.value < props.text.length) {
      displayText.value = displayText.value
        .map((l, i) =>
          l === " "
            ? l
            : i <= iterations.value
              ? props.text[i]
              : getRandomLetter(),
        )
        .filter((l) => l !== undefined);
      iterations.value += 0.1;
    } else {
      pause();
    }
  },
  computed(() => props.duration / (props.text.length * 10)),
);

const startAnimation = () => {
  pause();
  resume();
};

watch(
  () => props.text,
  (newText) => {
    displayText.value = newText.split("");
    triggerAnimation();
  },
);

if (props.animateOnLoad) {
  triggerAnimation();
}
</script>
