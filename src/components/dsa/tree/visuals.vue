<template>
  <div class="absolute bottom-0">
    <TreeNode :node="(root as node)" />
  </div>
</template>
<script setup lang="ts">
import { onMounted, ref, watch } from "vue";
import TreeNode from "./treeNode.vue";

const props = defineProps({
  input: {
    type: Number,
    default: 0,
  },
  treeLength: {
    type: Number,
    default: 0,
  },
});

watch(
  () => props.treeLength,
  (newValue, oldValue) => {
    if (newValue > oldValue) {
      add();
    } else {
      remove();
    }
  }
);

class node {
  value: number | null;
  left: node | null;
  right: node | null;
  constructor(val: any) {
    this.value = val;
    this.left = null;
    this.right = null;
  }
}
const root = ref<node | null>(null);
const tree = ref<node[] | null[]>([]);

const add = () => {
  let flag = true;
  if (props.input == null) flag = false;
  const newNode = new node(props.input);
  (tree.value as node[]).forEach((val) => {
    if (val.value == props.input) {
      flag = false;
    }
  });
  if (flag) {
    (tree.value as node[]).push(newNode);

    if (!root.value) {
      root.value = newNode;
    } else {
      let leaf = root.value;
      let temp = root.value;
      while (temp != null) {
        if ((temp.value as number) > (newNode.value as number)) {
          leaf = temp;
          temp = temp.left as node;
        } else if ((temp.value as number) < (newNode.value as number)) {
          leaf = temp;
          temp = temp.right as node;
        }
      }

      if ((leaf.value as number) > (newNode.value as number)) {
        leaf.left = newNode;
      } else if ((leaf.value as number) < (newNode.value as number)) {
        leaf.right = newNode;
      }
    }
  }
};
const remove = () => {
  let flag = true;
  if (props.input == null || tree.value.length == 0) flag = false;
  flag = false;
  (tree.value as node[]).forEach((val) => {
    if (val.value == props.input) {
      flag = true;
    }
  });
  if (flag) {
    if (
      root.value?.value == props.input &&
      root.value.right == null &&
      root.value.left == null
    ) {
      root.value = null;
    } else {
      let leaf = root.value;
      let tempNode = null;
      while (leaf?.value != props.input) {
        if (((leaf as node).value as number) > props.input) {
          tempNode = leaf;
          leaf = leaf?.left as node;
        } else {
          tempNode = leaf;
          leaf = leaf?.right as node;
        }
      }
      let tempVal = null;

      while (leaf != null) {
        if (leaf.left != null) {
          tempVal = leaf.value;
          leaf.value = leaf.left?.value;
          leaf.left.value = tempVal;
          tempNode = leaf;
          leaf = leaf.left;
        } else if (leaf.right != null) {
          tempVal = leaf.value;
          leaf.value = leaf.right?.value;
          leaf.right.value = tempVal;
          tempNode = leaf;
          leaf = leaf.right;
        } else {
          if (tempNode?.left?.value == props.input) {
            tempNode.left = null;
          } else if (tempNode?.right?.value == props.input) {
            tempNode.right = null;
          }
          leaf = null;
        }
      }
    }
    tree.value.forEach((n, index) => {
      if (props.input == n?.value) {
        (tree.value[index] as node).value = null;
      }
    });
  }
};
onMounted(() => {});
</script>
