<template>
  <div class="flex items-center">
    <span class="text-xl font-medium text-slate- m-4">Some Random Menu</span>
    <button class="flex items-center" @click="stepperCount++">
      <span class="material-symbols-outlined text-sky-500">
        keyboard_double_arrow_down
      </span>
    </button>
  </div>
  <div v-for="count in stepperCount">
    <Stepper
      :stepperCount="stepperCount"
      :stepNumber="count"
      :class="{ 'has-line': count !== 1 }"
    />
  </div>
  <button
    class="bg-green-600 shadow-lg py-3 px-4 hover:bg-green-700 duration-300 text-white fixed bottom-7 right-10 rounded-md"
  >
    Submit Stepper
  </button>
</template>

<script setup>
import { ref, inject } from 'vue';
import Stepper from './components/Stepper.vue';

const emitter = inject('emitter');

emitter.on('add-stepper', () => {
  stepperCount.value++;
});

emitter.on('remove-stepper', () => {
  stepperCount.value--;
});

let stepperCount = ref(1);
</script>

<style scoped>
.has-line {
  position: relative;
}
.has-line::after {
  content: '';
  position: absolute;
  top: -70px;
  left: 37px;
  width: 5px;
  height: 120px;
  background: rgb(159, 224, 250);
}
</style>
