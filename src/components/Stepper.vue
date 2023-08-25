<template>
  <div class="stepper-container">
    <!-- <pre>{{ stepper }}</pre> -->
    <button
      type="button"
      :disabled="step !== steppers.length"
      class="add-stepper"
      @click="emitAddEvent()"
    >
      <span class="material-symbols-outlined">
        keyboard_double_arrow_down
      </span>
    </button>
    <button type="button" class="remove-stepper" @click="deleteStepper">
      <span class="material-symbols-outlined">delete </span>
    </button>
    <h3 class="text-sky-400 font-semibold text-lg">
      Step {{ step }}:
      <i> {{ steppers[indexOfThisStepper].stepperName }} selection</i>
    </h3>
    <div class="primary border-1 rounded-sm border-slate-400">
      <div class="fields type">
        <label class="required" for="">Type</label>
        <select
          name=""
          id=""
          v-model="steppers[indexOfThisStepper].stepperType"
        >
          <option value="base">Base</option>
          <option value="size">Size</option>
          <option value="addOn">Add On</option>
        </select>
      </div>
      <div class="fields name">
        <label class="required" for="">Name</label>
        <input type="text" v-model="currentStepper.stepperName" />
      </div>
      <div class="fields min">
        <label class="required" for="">Min</label>
        <input type="number" v-model="currentStepper.minValue" min="0" />
      </div>
      <div class="fields max">
        <label class="required" for="">Max</label>
        <input type="number" v-model="currentStepper.maxValue" min="0" />
      </div>
      <div class="fields description">
        <label for="">Description</label>
        <input type="text" name="" id="" v-model="currentStepper.description" />
      </div>
    </div>
    <Option />
  </div>
</template>

<script setup>
import { inject, watch } from 'vue';
import Option from './Option.vue';

const props = defineProps({
  stepper: Object,
  step: Number,
});
const emitter = inject('emitter');
const steppers = inject('steppers');

const indexOfThisStepper = steppers.value.findIndex((item) => {
  return item.id === props.stepper.id;
});
const currentStepper = steppers.value[indexOfThisStepper];

// console.log(indexOfThisStepper);

const emitAddEvent = () => {
  emitter.emit('add-stepper');
};

const deleteStepper = () => {
  if (indexOfThisStepper === -1) {
    console.log('No steppers of such id found!');
    return;
  }
  console.log(indexOfThisStepper);
  steppers.value.splice(indexOfThisStepper, 1);
};
</script>

<style scoped>
@keyframes pump {
  0% {
    scale: 1;
    transform: translateY(-50%);
  }
  50% {
    scale: 0.95;
    transform: translateY(-35%);
  }
  100% {
    scale: 1;
    transform: translateY(-50%);
  }
}
.stepper-container {
  --blue: rgb(26, 145, 249);
  background: #e9f2ff;
  border: 2px dashed #c8c8c8;
  border-radius: 5px;
  position: relative;
  padding: 1em 0.5em 0.5em 6em;
  width: 80%;
  margin: 2em auto;
}

.add-stepper {
  position: absolute;
  z-index: 10;
  font-size: 18px;
  display: grid;
  place-items: center;
  color: var(--blue);
  background: white;
  border: 1.4px dotted var(--blue);
  box-shadow: 0 5px 8px rgba(0, 0, 0, 0.18);
  width: 40px;
  aspect-ratio: 1;
  border-radius: 50%;
  left: 20px;
  top: 50%;
  transform: translateY(-50%);
  transition: all 400ms ease;
}

.remove-stepper {
  display: grid;
  place-items: center;
  background: #e43737;
  width: 25px;
  aspect-ratio: 1;
  border-radius: 50%;
  right: 10px;
  top: 10px;
  position: absolute;
  color: white;
  transition: background 400ms ease;
}
.remove-stepper > span {
  font-size: 14px;
}
.remove-stepper:hover {
  transition: background 400ms ease;
  background: #c42f2f;
}
.add-stepper:disabled {
  background-color: var(--blue);
  color: white;
  border: 2px solid white;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  cursor: not-allowed;
}
.add-stepper:not(.add-stepper:disabled) {
  animation: pump 1.5s ease infinite;
}
.add-stepper:not(.add-stepper:disabled):hover {
  background: rgb(0, 133, 0);
  transition: all 400ms ease;
}
.primary {
  border: 1px solid #c8c8c8;
  border-radius: 5px;
  padding: 0.5em;
  display: flex;
  gap: 5px;
}

.fields label {
  color: #7a7a7a;
  display: block;
}
.fields input,
.fields select {
  min-width: none;
  min-height: none;
  padding: 5px 10px;
  border: 1px solid #d4d4d4;
  border-radius: 5px;
  width: 100%;
}
.type {
  flex-basis: 15%;
}
.name {
  flex-basis: 20%;
}
.min {
  flex-basis: 8%;
}
.max {
  flex-basis: 8%;
}
.description {
  flex: 1;
}
</style>
