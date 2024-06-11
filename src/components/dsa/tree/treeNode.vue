<template>
  <div class="flex flex-col items-center">
    <div>
      <div class="flex flex-col">
        <div
          class="h-12 w-12 border-2 flex justify-center items-center shadow-sm rounded-full bg-white z-10"
          v-if="node != null"
        >
          {{ node?.value }}
        </div>
        <hr
          v-if="node?.left!=null&&node?.right!"
          class="transform rotate-90 mt-[22px]"
        />
      </div>
    </div>
    <div class="flex justify-center gap-0 relative">
      <div v-if="node?.left">
        <TreeNode :node="node.left" class="mr-6" />
      </div>
      <hr
        v-if="node?.left && node?.right"
        class="absolute w-[60%] top-[22px]"
        :style="getLength"
      />
      <div v-if="node?.right">
        <TreeNode :node="node.right" class="ml-6" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
const props = defineProps({
  node: Object,
});

const leftClass = ref("");
const rightClass = ref("");

const getLength = computed(() => {
  const leftCount = getLeafCount(props.node?.left);
  const rightCount = getLeafCount(props.node?.right);
  if (leftCount > rightCount) {
    return {
      marginLeft: `${(leftCount - rightCount) * 20}px`,
    };
  } else if (rightCount > leftCount) {
    return {
      marginRight: `${(rightCount - leftCount) * 20}px`,
    };
  } else return null;
});
const getLeafCount = (node: any): number => {
  if (node != null) {
    return getLeafCount(node.right) + getLeafCount(node.left);
  } else {
    return 1;
  }
};
onMounted(() => {});
</script>
