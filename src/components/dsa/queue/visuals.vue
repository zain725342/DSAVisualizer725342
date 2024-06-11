<template>
  <div class="absolute bottom-0 flex">
    <div v-for="val in queue">
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
import { onMounted, ref, watch } from "vue";

const props = defineProps({
  input: {
    type: Number,
    default: 0,
  },
  queueLength: {
    type: Number,
    default: 0,
  },
});

watch(
  () => props.queueLength,
  (newValue, oldValue) => {
    if (newValue > oldValue) {
      enqueue();
    } else {
      dequeue();
    }
  }
);

const queue = ref<number[] | null[]>(new Array(10).fill(null));
const queueIndex = ref(0);

const enqueue = () => {
  if (queueIndex.value < 10) {
    queue.value[queueIndex.value] = props.input;
    queueIndex.value++;
  }
};
const dequeue = () => {
  if (queueIndex.value > 0) {
    queue.value[0] = null;
    let temp = 0;
    for (let i = 0; i < queue.value.length - 1; i++) {
      queue.value[i] = queue.value[i + 1];
    }
    queue.value[queue.value.length - 1] = null;
    queueIndex.value--;
  }
};
onMounted(() => {});
</script>
