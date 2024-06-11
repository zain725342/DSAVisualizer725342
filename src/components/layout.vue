<script setup lang="ts"></script>

<template>
  <div class="flex h-screen">
    <div class="w-[20%] bg-slate-100 justify-around flex flex-col px-4">
      <slot name="options"></slot>
      <slot name="controls"></slot>
      <slot name="info"></slot>
    </div>
    <div class="w-[80%] flex flex-col">
      <div class="h-[80%] relative flex justify-center">
        <slot name="visuals"></slot>
      </div>
      <div class="h-[20%] border-t-2"></div>
    </div>
  </div>
</template>
