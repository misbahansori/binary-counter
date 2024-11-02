<script setup lang="ts">
import emblaCarouselVue from "embla-carousel-vue";

const { digit, digits } = defineProps<{
  digit: string;
  digits: string[];
}>();

const [emblaRef, emblaApi] = emblaCarouselVue({
  axis: "y",
  loop: true,
});

watch(
  () => digit,
  () => {
    const index = digits.indexOf(digit);

    if (index === -1) return;

    emblaApi.value?.scrollTo(index);
  },
);
</script>

<template>
  <div class="overflow-hidden" ref="emblaRef">
    <div class="flex h-12 flex-col">
      <div
        v-for="digit in digits"
        :key="digit"
        class="flex h-12 w-8 min-w-0 flex-[0_0_100%] items-center justify-center font-orbitron text-3xl font-bold text-white"
      >
        {{ digit }}
      </div>
    </div>
  </div>
</template>
