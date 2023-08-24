<template>
  <div class="stepper-container">
    <button
      type="button"
      :disabled="stepNumber !== stepperCount"
      class="add-stepper"
      @click="emitAddEvent"
    >
      <!-- <span>{{ stepNumber }}</span> -->
      <span class="material-symbols-outlined">
        keyboard_double_arrow_down
      </span>
    </button>
    <button type="button" class="remove-stepper" @click="emitDeleteEvent">
      <span class="material-symbols-outlined">delete </span>
    </button>
    <h3 class="text-sky-400 font-semibold text-lg">
      Step {{ stepNumber }}: <i> {{ name }} Selection</i>
    </h3>
    <div class="primary border-1 rounded-sm border-slate-400">
      <div class="fields type">
        <label class="required" for="">Type</label>
        <select name="" id="">
          <option value="">Size</option>
          <option value="">Base</option>
          <option value="">Add On</option>
        </select>
      </div>
      <div class="fields name">
        <label class="required" for="">Name</label>
        <input type="text" v-model="name" name="" id="" />
      </div>
      <div class="fields min">
        <label class="required" for="">Min</label>
        <input type="number" name="" id="" min="0" />
      </div>
      <div class="fields max">
        <label class="required" for="">Max</label>
        <input type="number" name="" id="" min="0" />
      </div>
      <div class="fields description">
        <label for="">Description</label>
        <input type="text" name="" id="" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { inject, ref } from 'vue';
const emitter = inject('emitter');

const emitAddEvent = () => {
  emitter.emit('add-stepper');
};

const emitDeleteEvent = () => {
  emitter.emit('remove-stepper');
};

const name = ref('');

const props = defineProps({
  stepNumber: Number,
  stepperCount: Number,
});
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
  position: relative;
  border: 2px dashed rgb(200, 200, 200);
  border-radius: 5px;
  padding: 1em 0.25em 0.25em 6em;
  width: 80%;
  margin: 2em auto;
}

.add-stepper {
  position: absolute;
  z-index: 10;
  font-size: 18px;
  display: grid;
  place-items: center;
  color: white;
  background: rgb(0, 162, 0);
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
  width: 35px;
  aspect-ratio: 1;
  border-radius: 50%;
  right: 20px;
  top: 20px;
  position: absolute;
  color: white;
  transition: background 400ms ease;
}
.remove-stepper > span {
  font-size: 18px;
}
.remove-stepper:hover {
  transition: background 400ms ease;
  background: #c42f2f;
}
.add-stepper:disabled {
  background-color: #c0c0c0;
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

.required::after {
  content: '*';
  color: rgb(253, 110, 110);
  margin-left: 5px;
  font-weight: bold;
}
</style>
