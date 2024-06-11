<template>
  <div class="flex">
    <div
      v-if="node != null"
      class="h-12 w-12 border-2 rounded-md flex justify-center items-center shadow-sm"
    >
      {{ node.value }}
    </div>
    <div v-if="node?.next != null" class="flex items-center">
      <span class="text-2xl text-gray-300">-></span>
      <listNode :node="node.next" />
    </div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  node: Object,
});
</script>
