<template>
  <div class="absolute bottom-0">
    <div v-for="val in stack">
      <div
        v-if="val != null"
        class="h-12 w-12 border-2 flex justify-center items-center shadow-sm"
      >
        {{ val }}
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, watch } from "vue";

const props = defineProps({
  input: {
    type: Number,
    default: 0,
  },
  stackLength: {
    type: Number,
    default: 0,
  },
});

watch(
  () => props.stackLength,
  (newValue, oldValue) => {
    if (newValue > oldValue) {
      push();
    } else {
      pop();
    }
  }
);

const stack = ref<number[] | null[]>(new Array(10).fill(null));
const stackIndex = ref(stack.value.length - 1);

const push = () => {
  if (stackIndex.value > 0) {
    stack.value[stackIndex.value] = props.input;
    stackIndex.value--;
  }
};
const pop = () => {
  if (stackIndex.value < 9) {
    stack.value[stackIndex.value + 1] = null;
    stackIndex.value++;
  }
};
</script>
