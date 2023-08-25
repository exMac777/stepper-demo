<template>
  <div class="secondary border-1 rounded-sm border-slate-400">
    <div class="fields title">
      <label class="required" for="">Option title</label>
      <input type="text" />
    </div>
    <div class="fields price">
      <label class="required" for="">Option price</label>
      <input type="number" min="0" />
    </div>
    <div class="fields sel-qty">
      <label class="required" for="">Enable quantity selection</label>
      <input class="checkbox" type="checkbox" />
    </div>
  </div>
</template>

<style scoped>
.secondary {
  width: 80%;
  margin: 5px 0 0 auto;
  border-radius: 5px;
  padding: 0.5em;
  border: 1px solid #c8c8c8;
  display: flex;
  gap: 5px;
}

.fields input:not(.checkbox) {
  min-width: none;
  min-height: none;
  padding: 5px 10px;
  border: 1px solid #d4d4d4;
  border-radius: 5px;
  width: 100%;
}
.title {
  flex-basis: 20%;
}
.price {
  flex-basis: 20%;
}

.sel-qty {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
.checkbox {
  border: 1px solid #d4d4d4;
  width: 25px;
  height: 25px;
  border-radius: 2px;
}
.fields label {
  color: #7a7a7a;
  display: block;
}
</style>
