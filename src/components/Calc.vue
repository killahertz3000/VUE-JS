<template>
  <div>
    <div class="display">
      <input type="number" v-model="operand1" />
      <input type="number" v-model="operand2" />
      <div class="display__result" v-show="!error">
      = {{ result }}
    </div>
     <div class="display__error" v-show="error">Ошибка! {{ error }}</div>
      <div class="display__messages">
        <template v-if="result === null"></template>
        <template v-else-if="result < 0"> Получилось отрицательное число. </template>
        <template v-else-if="result < 100">Результат в первой сотне.</template>
        <template v-else>Получилось слишком большое число.</template>
      </div>
    </div>
    <div class="keyboard">
      <button
        type="button"
        v-for="operation in operations"
        :key="operation.char"
        :title="operation.title"
        @click="calculate(operation.char)"
      >
        {{ operation.char }}
      </button>
    </div>
    <div>
      <input
        id="control"
        type="checkbox"
        v-model="showScreenKeyboard"
      />
      <label>Отобразить экранную клавиатуру</label
      >
    </div>
        <div class="screen-keyboard" v-show="showScreenKeyboard">
      <div>
        <button
          type="button"
          v-for="button in screenKeyboard"
          :key="button.char"
          :title="button.title"
          @click="inputScreenKeyboard(button.char)"
        >
          {{ button.char }}
        </button>
        <button
          type="button"
          title="Удалить"
          @click="deleteScreenKeyboard"
        >
          &#8592;
        </button>
      </div>
      <input
        id="operand1"
        type="radio"
        name="fieldSelection"
        value="operand1"
        v-model="selectedOperand"
        checked
      />
      <label for="operand1">Операнд 1</label>
      <input
        id="operand2"
        type="radio"
        name="fieldSelection"
        value="operand2"
        v-model="selectedOperand"
      />
      <label for="operand2">Операнд 2</label>
    </div>
  </div>
</template>
<script>

export default {
  name: 'Calc',
  data() {
    return {
      operations: [
        { char: '+', title: 'Сложение' },
        { char: '-', title: 'Вычитаение' },
        { char: '*', title: 'Умножение' },
        { char: '/', title: 'Деление' },
        { char: '//', title: 'Целочисленное деление' },
        { char: '**', title: 'Возведение в степернь' },
      ],
      operand1: 0,
      operand2: 0,
      result: null,
      error: '',
      showScreenKeyboard: false,
      selectedOperand: 'operand1',
      screenKeyboard: [
        { char: '0', title: '0' },
        { char: '1', title: '1' },
        { char: '2', title: '2' },
        { char: '3', title: '3' },
        { char: '4', title: '4' },
        { char: '5', title: '5' },
        { char: '6', title: '6' },
        { char: '7', title: '7' },
        { char: '8', title: '8' },
        { char: '9', title: '9' },
      ],
    };
  },
  methods: {
    sum() {
      this.result = this.operand1 + this.operand2;
    },
    sub() {
      this.result = this.operand1 - this.operand2;
    },
    mult() {
      this.result = this.operand1 * this.operand2;
    },
    div() {
      if (this.operand2 === 0) {
        this.error = 'Деление на ноль.';
      } else {
        this.result = this.operand1 / this.operand2;
      }
    },
    integerDiv() {
      if (this.operand2 === 0) {
        this.error = 'Деление на ноль.';
      } else {
        this.result = Math.floor(this.operand1 / this.operand2);
      }
    },
    pow() {
      this.result = this.operand1 ** this.operand2;
    },
    calculate(operation = '+') {
      this.error = '';
      switch (operation) {
        case '+':
          this.sum();
          break;
        case '-':
          this.sub();
          break;
        case '*':
          this.mult();
          break;
        case '/':
          this.div();
          break;
        case '//':
          this.integerDiv();
          break;
        case '**':
          this.pow();
          break;
        default:
          break;
      }
    },
    inputScreenKeyboard(char) {
      const operand = this.selectedOperand;
      const value = String(this[operand]);
      this[operand] = Number(value + char);
    },
    deleteScreenKeyboard() {
      const operand = this.selectedOperand;
      this[operand] = Math.trunc(this[operand] / 10);
    },
  },
};
</script>
