<template>
  <div class="flex flex-col gap-4">
    <Input type="number" v-model="addInput" placeholder="Enter a number" />
    <Button
      @click="
        emit('enlist', addInput);
        addInput = null;
      "
      >Enlist</Button
    >
    <Input type="number" v-model="removeInput" placeholder="Enter a number" />
    <Button
      @click="
        emit('delist', removeInput);
        removeInput = null;
      "
      >Delist</Button
    >
  </div>
</template>
<script setup lang="ts">
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { ref } from "vue";

const emit = defineEmits(["enlist", "delist"]);

const addInput = ref<number | null>(null);
const removeInput = ref<number | null>(null);
</script>
