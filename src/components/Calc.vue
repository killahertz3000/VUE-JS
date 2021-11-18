<template>
  <div>
    <div class="display">
      <input type="number" v-model="operand1" />
      <input type="number" v-model="operand2" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button @click="result = operand1 + operand2">+</button>
      <button @click="result = operand1 - operand2">-</button>
      <button @click="result = operand1 / operand2">/</button>
      <button @click="result = operand1 * operand2">*</button>
      <button @click="result = Math.pow(operand1, operand2)">**</button>
      <button @click="result = Math.floor(operand1 / operand2)">//</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Calc',
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
    };
  },
};
</script>
