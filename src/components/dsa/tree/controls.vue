<template>
  <div class="flex flex-col gap-4">
    <Input type="number" v-model="addInput" placeholder="Enter a number" />
    <Button
      @click="
        emit('add', addInput);
        addInput = null;
      "
      >Add</Button
    >
    <Input type="number" v-model="removeInput" placeholder="Enter a number" />
    <Button
      @click="
        emit('remove', removeInput);
        removeInput = null;
      "
      >remove</Button
    >
  </div>
</template>
<script setup lang="ts">
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { ref } from "vue";

const emit = defineEmits(["add", "remove"]);

const addInput = ref<number | null>(null);
const removeInput = ref<number | null>(null);
</script>
