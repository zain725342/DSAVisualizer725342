<template>
  <div class="flex flex-col gap-4">
    <Input type="number" v-model="input" placeholder="Enter a number" />
    <Button
      @click="
        emit('push', input);
        input = null;
      "
      >Push</Button
    >
    <Button @click="emit('pop')">Pop</Button>
  </div>
</template>
<script setup lang="ts">
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { ref } from "vue";

const emit = defineEmits(["push", "pop"]);

const input = ref<number | null>(null);
</script>
