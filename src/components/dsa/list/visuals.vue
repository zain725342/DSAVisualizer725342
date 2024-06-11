<template>
  <div class="absolute bottom-0 flex">
    <ListNode :node="head" />
  </div>
</template>
<script setup lang="ts">
import ListNode from "./listNode.vue";
import { onMounted, ref, watch } from "vue";

const props = defineProps({
  input: {
    type: Number,
    default: 0,
  },
  listLength: {
    type: Number,
    default: 0,
  },
});

watch(
  () => props.listLength,
  (newValue, oldValue) => {
    if (newValue > oldValue) {
      enlist();
    } else {
      delist();
    }
  }
);

class node {
  value: number;
  next: node | null;
  constructor(val: any) {
    this.value = val;
    this.next = null;
  }
}
const head = ref<node | null>(null);
const list = ref<node[] | null[]>([]);

const enlist = () => {
  if (props.input == null) return;
  const newNode = new node(props.input);
  (list.value as node[]).push(newNode);
  if (!head.value) {
    head.value = newNode;
  } else {
    let temp = head.value;
    while (temp.next != null) {
      temp = temp.next;
    }
    temp.next = newNode;
  }
};
const delist = () => {
  if (props.input == null) return;
  if (!head.value) {
    return;
  } else if (head.value.value == props.input) {
    head.value = head.value.next;
  } else {
    let prevTemp = null as node | null;
    let currentTemp = head.value as node | null;
    while (currentTemp?.next != null) {
      prevTemp = currentTemp;
      currentTemp = currentTemp.next;
      if (currentTemp.value == props.input) {
        prevTemp.next = currentTemp.next;
        currentTemp = null;
      }
    }
    if (Number(currentTemp?.value) == props.input) {
      currentTemp = null;
      if (prevTemp?.next != null) {
        prevTemp.next = null;
      }
    }
  }
  list.value.forEach((n, index) => {
    if (n?.value == props.input) {
      list.value[index] = null;
    }
  });
};
onMounted(() => {});
</script>
