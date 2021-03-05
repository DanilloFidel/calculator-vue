<template>
  <div class="calculator">
    <div class="calculator__display output">
      {{ displayResult }}
    </div>
    <div class="calculator__button-area">
      <div
        v-for="(btn, idx) in buttons"
        :key="`btn-${idx}`"
        :class="[btn.className, 'calculator__button']"
        @click="runFn(btn.functionName, btn.value)"
      >
        {{ btn.value }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    countValue: '',
    displayResult: null,
    buttons: [
      {
        value: '7',
        className: 'digit-7',
        functionName: 'handleDigit',
      },
      {
        value: '8',
        className: 'digit-8',
        functionName: 'handleDigit',
      },
      {
        value: '9',
        className: 'digit-9',
        functionName: 'handleDigit',
      },
      {
        value: '/',
        className: 'op-div',
        functionName: 'handleOperator',
      },
      {
        value: '4',
        className: 'digit-4',
        functionName: 'handleDigit',
      },
      {
        value: '5',
        className: 'digit-5',
        functionName: 'handleDigit',
      },
      {
        value: '6',
        className: 'digit-6',
        functionName: 'handleDigit',
      },
      {
        value: '*',
        className: 'op-mul',
        functionName: 'handleOperator',
      },
      {
        value: '3',
        className: 'digit-3',
        functionName: 'handleDigit',
      },
      {
        value: '2',
        className: 'digit-2',
        functionName: 'handleDigit',
      },
      {
        value: '1',
        className: 'digit-1',
        functionName: 'handleDigit',
      },
      {
        value: '-',
        className: 'op-sub',
        functionName: 'handleOperator',
      },
      {
        value: '0',
        className: 'digit-0',
        functionName: 'handleDigit',
      },
      {
        value: '+',
        className: 'op-add',
        functionName: 'handleOperator',
      },
      {
        value: '=',
        className: 'eq',
        functionName: 'evalResult',
      },
      {
        value: 'c',
        className: 'clear',
        functionName: 'clearDisplay',
      },
    ],
  }),

  methods: {
    runFn(fn, param) {
      this[fn](param)
    },
    evalResult() {
      if (this.lastDigitIsNumber(this.displayResult)) {
        const result = Math.floor(eval(this.displayResult))

        this.displayResult = Number.isFinite(result) ? result : ''
      }
    },
    clearDisplay() {
      this.displayResult = ''
    },
    handleDigit(value) {
      this.setDisplay(`${value}`)
    },
    handleOperator(value) {
      this.displayResult = value
    },
    setDisplay(val) {
      this.displayResult = `${this.displayResult}${val}`
    },
    isDigitNumber(val) {
      return Array(10)
        .fill()
        .map((item, i) => `${i}`)
        .includes(val)
    },
    lastDigitIsNumber(val) {
      return Array(10)
        .fill()
        .map((item, i) => `${i}`)
        .includes(val[val.length - 1])
    },
  },
}
</script>

<style>
.calculator {
  height: 500px;
  width: 300px;
  border: 5px solid;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  padding: 0 10px;
}

.calculator__display {
  height: 18%;
  background-color: rgba(203, 255, 207, 0.897);
}

.calculator__button {
  box-shadow: 0 2px 5px 1px rgb(64 60 67 / 16%);
  background-color: #bbbbbb;
  width: 71px;
  height: 24%;
}

.calculator__button-area {
  height: 78%;
  justify-content: space-around;
  flex-wrap: wrap;
  display: flex;
}
</style>
