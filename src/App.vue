<script setup lang="ts">
import Toaster from "@/components/ui/toast/Toaster.vue";
import layout from "@/components/layout.vue";
import stackControls from "./components/dsa/stack/controls.vue";
import stackVisuals from "./components/dsa/stack/visuals.vue";
import queueControls from "./components/dsa/queue/controls.vue";
import queueVisuals from "./components/dsa/queue/visuals.vue";
import listControls from "./components/dsa/list/controls.vue";
import listVisuals from "./components/dsa/list/visuals.vue";
import treeControls from "./components/dsa/tree/controls.vue";
import treeVisuals from "./components/dsa/tree/visuals.vue";

import { ref } from "vue";
import { Button } from "./components/ui/button";
import { useToast } from "@/components/ui/toast/use-toast";

const { toast } = useToast();

const option = ref("stack");
const limit = ref(9);

const input = ref<number | undefined>(0);
const length = ref(0);

const addValue = (val?: number) => {
  if (length.value < limit.value) {
    input.value = val;
    length.value++;
    console.log(length.value);
  } else {
    toast({
      title: "Warning!",
      description: "Input limit exceeded",
    });
  }
};
const removeValue = (val?: number) => {
  if (length.value > 0) {
    input.value = val;
    length.value--;
    console.log(length.value);
  } else {
    toast({
      title: "Warning!",
      description: "Structure is empty",
    });
  }
};
</script>

<template>
  <Toaster />
  <div>
    <layout>
      <template #options>
        <div class="flex flex-col gap-2">
          <Button
            @click="
              option = 'stack';
              limit = 9;
              length = 0;
            "
            >Stack</Button
          >
          <Button
            @click="
              option = 'queue';
              limit = 10;
              length = 0;
            "
            >Queue</Button
          >
          <Button
            @click="
              option = 'list';
              limit = 15;
              length = 0;
            "
            >Linked list</Button
          >
          <Button
            @click="
              option = 'tree';
              limit = 15;
              length = 0;
            "
            >Binary search tree</Button
          >
        </div>
      </template>
      <template #controls>
        <stackControls
          v-if="option == 'stack'"
          @push="addValue($event)"
          @pop="removeValue()"
        />
        <queueControls
          v-else-if="option == 'queue'"
          @enqueue="addValue($event)"
          @dequeue="removeValue()"
        />
        <listControls
          v-else-if="option == 'list'"
          @enlist="addValue($event)"
          @delist="removeValue($event)"
        />
        <treeControls
          v-else-if="option == 'tree'"
          @add="addValue($event)"
          @remove="removeValue($event)"
        />
      </template>
      <template #info>
        <div class="flex flex-col gap-2">
          <ul class="text-sm text-gray-600">
            <li>Structure limit is {{ limit }} elements max</li>
          </ul>
        </div>
      </template>
      <template #visuals>
        <stackVisuals
          v-if="option == 'stack'"
          :input="input"
          :stackLength="length"
        />
        <queueVisuals
          v-else-if="option == 'queue'"
          :input="input"
          :queueLength="length"
        />
        <listVisuals
          v-else-if="option == 'list'"
          :input="input"
          :listLength="length"
        />
        <treeVisuals
          v-else-if="option == 'tree'"
          :input="input"
          :treeLength="length"
        />
      </template>
    </layout>
  </div>
</template>
