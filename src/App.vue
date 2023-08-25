<template>
  <div class="flex items-center">
    <span class="text-xl font-medium text-slate-700 m-4">Some Random Menu</span>
    <button class="flex items-center" @click="addStepper">
      <span class="material-symbols-outlined text-sky-500">
        keyboard_double_arrow_down
      </span>
    </button>
  </div>

  <div class="steppers-container">
    <!-- Bunch of steppers -->
    <div v-for="(stepper, index) in steppers">
      <Stepper :stepper="stepper" :step="index + 1" class="stepper" />
      <!-- <pre>{{ stepper }}</pre> -->
    </div>
  </div>
  <button
    class="bg-green-600 shadow-lg py-3 px-4 hover:bg-green-700 duration-300 text-white fixed bottom-7 right-10 rounded-md"
    @click="submit"
  >
    Submit Stepper
  </button>
</template>

<script setup>
import { ref, inject, provide } from 'vue';
import Stepper from './components/Stepper.vue';

const emitter = inject('emitter');

emitter.on('add-stepper', (e) => {
  addStepper();
});

emitter.on('remove-stepper', (stepNum) => {
  steppers.value.splice(stepNum - 1, 1);
});

let id = 0;

function objectCreator(id) {
  return {
    id: id,
    stepperType: '',
    stepperName: '',
    minValue: '',
    maxValue: '',
    description: '',
  };
}
const steppers = ref([]);

function addStepper() {
  id++;
  const obj = objectCreator(id);
  steppers.value.push(obj);
  // console.log(steppers.value);
}

function submit() {
  console.log({
    menuCategory: 'pizza',
    id: 2,
    type: steppers.value.map((item) => {
      return { ...item };
    }),
  });
}

provide('steppers', steppers);
</script>

<style scoped>
/* .steppers-container {
  width: fit-content;
  margin-inline: auto;
  border: 2px dashed #c8c8c8;
  border-radius: 5px;
  background: #e9f2ff;
} */
.stepper:not(:first-of-type) {
  position: relative;
}
.stepper:not(:first-of-type)::after {
  content: '';
  position: absolute;
  top: -70px;
  left: 37px;
  width: 5px;
  height: 120px;
  background: rgb(159, 224, 250);
}
</style>
